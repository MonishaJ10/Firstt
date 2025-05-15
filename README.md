ParseService.java
package com.example.parser.service;

import org.springframework.stereotype.Service;

import java.io.*;
import java.nio.file.Files;
import java.nio.file.Paths;
import java.util.LinkedHashMap;
import java.util.Map;

@Service
public class ParseService {

    public File parseDesisToCsv(String filePath) throws IOException {
        String content = new String(Files.readAllBytes(Paths.get(filePath))).replace("\n", " ").replace("\r", " ");

        // Extract fixed fields
        String typeNature = content.substring(0, 2);
        String siteCode = content.substring(2, 6);
        String applicationCode = content.substring(6, 14);
        String instrumentCode = content.substring(14, 18);

        Map<String, String> dataMap = new LinkedHashMap<>();
        dataMap.put("TypeNature", typeNature);
        dataMap.put("SiteCode", siteCode);
        dataMap.put("ApplicationCode", applicationCode);
        dataMap.put("InstrumentCode", instrumentCode);

        // Parse remaining key-value pairs
        String remaining = content.substring(18);
        String[] parts = remaining.split("[ *]");

        for (String part : parts) {
            if (part.contains(":")) {
                String[] kv = part.split(":", 2);
                if (kv.length == 2) {
                    dataMap.put(kv[0], kv[1]);
                }
            }
        }

        // Write to CSV file
        File csvOutput = File.createTempFile("parsed_output", ".csv");
        try (BufferedWriter writer = new BufferedWriter(new FileWriter(csvOutput))) {
            writer.write(String.join(",", dataMap.keySet()));
            writer.newLine();
            writer.write(String.join(",", dataMap.values()));
        }

        return csvOutput;
    }
}


 

-----------------
model/ParseRequest.java
package com.example.desisparser.model;

public class ParseRequest {
    private String desisData;

    public String getDesisData() {
        return desisData;
    }

    public void setDesisData(String desisData) {
        this.desisData = desisData;
    }
}

service/parse service.java
package com.example.desisparser.service;

import org.springframework.stereotype.Service;
import java.util.*;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

@Service
public class ParseService {

    public String convertToCsv(String desisData) {
        Map<String, String> dataMap = new LinkedHashMap<>();

        // Extract headers from first part (e.g., OP4035)
        String typeNature = desisData.substring(0, 2);
        String siteCode = desisData.substring(2, 6);
        String appCode = desisData.substring(6, 14);
        String instrumentCode = desisData.substring(14, 18);

        dataMap.put("TypeNature", typeNature);
        dataMap.put("SiteCode", siteCode);
        dataMap.put("ApplicationCode", appCode);
        dataMap.put("InstrumentCode", instrumentCode);

        // Regex to match *code:value or code:value patterns
        Pattern pattern = Pattern.compile("[*]?(\\d+):([^:*]+)");
        Matcher matcher = pattern.matcher(desisData);

        while (matcher.find()) {
            String key = matcher.group(1).trim();
            String value = matcher.group(2).trim();
            dataMap.put(key, value);
        }

        // Generate CSV
        StringBuilder csv = new StringBuilder();
        // Header row
        csv.append(String.join(",", dataMap.keySet())).append("\n");
        // Data row
        csv.append(String.join(",", dataMap.values())).append("\n");

        return csv.toString();
    }
}

controller/parser controller.java
package com.example.desisparser.controller;

import com.example.desisparser.model.ParseRequest;
import com.example.desisparser.service.ParseService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/api/parse")
public class ParseController {

    @Autowired
    private ParseService parseService;

    @PostMapping("/desis-to-csv")
    public String convertDesisToCsv(@RequestBody ParseRequest request) {
        return parseService.convertToCsv(request.getDesisData());
    }
}

desisparseapplication.java

package com.example.desisparser;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class DesisParserApplication {
    public static void main(String[] args) {
        SpringApplication.run(DesisParserApplication.class, args);
    }
}


Full Updated Spring Boot Code


---

Model: ParseRequest.java

package com.example.desisparser.model;

public class ParseRequest {
    private String desisData;

    public String getDesisData() {
        return desisData;
    }

    public void setDesisData(String desisData) {
        this.desisData = desisData;
    }
}


---

Service: ParseService.java

package com.example.desisparser.service;

import org.springframework.stereotype.Service;

import java.io.ByteArrayInputStream;
import java.io.ByteArrayOutputStream;
import java.io.PrintWriter;
import java.util.LinkedHashMap;
import java.util.Map;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

@Service
public class ParseService {

    public ByteArrayInputStream convertToCsvFile(String desisData) {
        Map<String, String> dataMap = new LinkedHashMap<>();

        // Extract first fields
        dataMap.put("Type Nature", desisData.substring(0, 2));
        dataMap.put("Site Code", desisData.substring(2, 6));
        dataMap.put("Application Code", desisData.substring(6, 14));
        dataMap.put("Instrument Code", desisData.substring(14, 18));

        String remaining = desisData.substring(18);

        // Match all *XX:value or XX:value pairs
        Pattern pattern = Pattern.compile("[*]?(\\d+):([^:*]+)");
        Matcher matcher = pattern.matcher(remaining);

        while (matcher.find()) {
            String key = matcher.group(1).trim();
            String value = matcher.group(2).trim();
            dataMap.put(key, value);
        }

        // Write to CSV in memory
        ByteArrayOutputStream out = new ByteArrayOutputStream();
        PrintWriter writer = new PrintWriter(out);

        // Header
        writer.println(String.join(",", dataMap.keySet()));
        // Values
        writer.println(String.join(",", dataMap.values()));

        writer.flush();
        return new ByteArrayInputStream(out.toByteArray());
    }
}


---

Controller: ParseController.java

package com.example.desisparser.controller;

import com.example.desisparser.model.ParseRequest;
import com.example.desisparser.service.ParseService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.core.io.InputStreamResource;
import org.springframework.http.HttpHeaders;
import org.springframework.http.MediaType;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/api/parse")
public class ParseController {

    @Autowired
    private ParseService parseService;

    @PostMapping("/desis-to-csv")
    public ResponseEntity<InputStreamResource> convertDesisToCsv(@RequestBody ParseRequest request) {
        var csvStream = parseService.convertToCsvFile(request.getDesisData());

        HttpHeaders headers = new HttpHeaders();
        headers.add("Content-Disposition", "attachment; filename=desis_data.csv");

        return ResponseEntity.ok()
                .headers(headers)
                .contentType(MediaType.parseMediaType("text/csv"))
                .body(new InputStreamResource(csvStream));
    }
}


---

Main Class: DesisParserApplication.java

package com.example.desisparser;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class DesisParserApplication {
    public static void main(String[] args) {
        SpringApplication.run(DesisParserApplication.class, args);
    }
}





1. Create Controller

Create a new Java class:

> src/main/java/com/example/desisparser/controller/DesisController.java



package com.example.desisparser.controller;

import com.example.desisparser.service.DesisService;
import jakarta.servlet.http.HttpServletResponse;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.*;

import java.io.IOException;

@RestController
@RequestMapping("/api/desis")
public class DesisController {

    @Autowired
    private DesisService desisService;

    @PostMapping("/parse")
    public void parseDesisData(@RequestBody String desisData, HttpServletResponse response) throws IOException {
        desisService.processDesisToCSV(desisData, response);
    }
}


---

2. Create Service

> src/main/java/com/example/desisparser/service/DesisService.java



package com.example.desisparser.service;

import org.springframework.stereotype.Service;

import jakarta.servlet.http.HttpServletResponse;
import java.io.PrintWriter;
import java.util.LinkedHashMap;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

@Service
public class DesisService {

    public void processDesisToCSV(String desisData, HttpServletResponse response) throws java.io.IOException {
        LinkedHashMap<String, String> csvData = new LinkedHashMap<>();

        // Extract header parts
        String typeNature = desisData.substring(0, 2);
        String siteCode = desisData.substring(2, 6);
        String appCode = extractAlpha(desisData.substring(6)).split("[0-9]")[0];
        String rem = desisData.substring(6 + appCode.length());
        String instrumentCode = extractAlpha(rem).split("[0-9]")[0];
        String remainingData = rem.substring(instrumentCode.length());

        csvData.put("type_nature", typeNature);
        csvData.put("site_code", siteCode);
        csvData.put("application_code", appCode);
        csvData.put("instrument_code", instrumentCode);

        // Extract remaining key:value pairs using regex
        Pattern pattern = Pattern.compile("(\\d+):([^\\s*]+)");
        Matcher matcher = pattern.matcher(remainingData);

        while (matcher.find()) {
            csvData.put(matcher.group(1), matcher.group(2));
        }

        // Prepare response for CSV download
        response.setContentType("text/csv");
        response.setHeader("Content-Disposition", "attachment; filename=\"parsed_output.csv\"");
        PrintWriter writer = response.getWriter();

        // Write CSV header
        writer.println(String.join(",", csvData.keySet()));

        // Write CSV values
        writer.println(String.join(",", csvData.values()));

        writer.flush();
        writer.close();
    }

    private String extractAlpha(String input) {
        return input.replaceAll("[^A-Za-z]", "");
    }
}


Parsecontroller.java
package com.example.desisparser.controller;

import com.example.desisparser.service.ParseService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.core.io.InputStreamResource;
import org.springframework.http.HttpHeaders;
import org.springframework.http.MediaType;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.*;

import java.io.IOException;
import java.io.InputStream;
import java.nio.file.Files;
import java.nio.file.Path;

@RestController
@RequestMapping("/api/parse")
public class ParseController {

    @Autowired
    private ParseService parseService;

    @PostMapping("/desis-to-csv")
    public ResponseEntity<InputStreamResource> convertDesisToCsv(@RequestBody String desisData) {
        var csvStream = parseService.convertToCsvFile(desisData);

        HttpHeaders headers = new HttpHeaders();
        headers.add("Content-Disposition", "attachment; filename=desis_data.csv");

        return ResponseEntity.ok()
                .headers(headers)
                .contentType(MediaType.parseMediaType("text/csv"))
                .body(new InputStreamResource(csvStream));
    }

    // For local testing with hardcoded file path
    @GetMapping("/test-local-file")
    public ResponseEntity<InputStreamResource> testLocalFile() throws IOException {
        // Replace this path with your actual file location
        String filePath = "C:/Users/YourName/Desktop/kondorfx.txt";

        // Read file content from local system
        String desisData = Files.readString(Path.of(filePath));

        var csvStream = parseService.convertToCsvFile(desisData);

        HttpHeaders headers = new HttpHeaders();
        headers.add("Content-Disposition", "attachment; filename=desis_data.csv");

        return ResponseEntity.ok()
                .headers(headers)
                .contentType(MediaType.parseMediaType("text/csv"))
                .body(new InputStreamResource(csvStream));
    }
}

Parse service.java
package com.example.desisparser.service;

import jakarta.servlet.http.HttpServletResponse;
import org.springframework.stereotype.Service;
import org.springframework.web.multipart.MultipartFile;

import java.io.IOException;
import java.io.PrintWriter;
import java.util.LinkedHashMap;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

@Service
public class ParseService {

    public void processDesisFileToCSV(MultipartFile file, HttpServletResponse response) throws IOException {
        String desisData = new String(file.getBytes());
        processDesisToCSV(desisData, response);
    }

    public void processDesisToCSV(String desisData, HttpServletResponse response) throws IOException {
        // Extract fixed fields
        String type = desisData.substring(0, 2);
        String siteCode = desisData.substring(2, 6);
        String appCode = desisData.substring(6, 14);
        String instrument = desisData.substring(14, 18);

        // Rest of string
        String rest = desisData.substring(18);

        // Use regex to find key:value pairs (e.g., 89:TREASUR-PA)
        Pattern pattern = Pattern.compile("(\\d+):([^:\\*]+)");
        Matcher matcher = pattern.matcher(rest);

        LinkedHashMap<String, String> csvMap = new LinkedHashMap<>();
        csvMap.put("type", type);
        csvMap.put("sitecode", siteCode);
        csvMap.put("appcode", appCode);
        csvMap.put("instrument", instrument);

        while (matcher.find()) {
            String key = matcher.group(1);
            String value = matcher.group(2);
            csvMap.put(key, value);
        }

        // Set CSV response headers
        response.setContentType("text/csv");
        response.setHeader("Content-Disposition", "attachment; filename=\"desis_output.csv\"");

        PrintWriter writer = response.getWriter();

        // Write CSV header
        writer.println(String.join(",", csvMap.keySet()));

        // Write values
        writer.println(String.join(",", csvMap.values()));

        writer.flush();
        writer.close();
    }
}

