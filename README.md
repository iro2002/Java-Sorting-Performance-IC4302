# Sorting Algorithm Performance Evaluator — Java 23 / Maven

**University of Colombo** | **Faculty of Technology** | **Department of ICT**  
**Course:** IC4302 – Programming III  

This is the **standard Maven version** of the Java Swing sorting assignment. The original algorithms and GUI are retained; the folder layout and automated tests have been upgraded. Each of the five sorting algorithms is neatly organized in its own file under the `sortbenchmark.algorithms` sub-package.

## Prerequisites on Windows

- **JDK 23** (not just a Java Runtime Environment). Check both commands:

  ```powershell
  java -version
  javac -version
  ```

- Maven 3.9+ **or** IntelliJ IDEA's bundled Maven support. Check Maven with `mvn -version` if running commands in PowerShell.

Your existing `java -version` output of **23.0.2** is suitable. If `javac -version` does not work, make sure the JDK's `bin` folder is on the system `PATH`. If `mvn -version` shows a different Java runtime, configure `JAVA_HOME` to your JDK 23 folder.

## Run with IntelliJ IDEA (recommended)

1. Extract the ZIP and open **IntelliJ IDEA**.
2. Choose **Open** and select the `Java-Sorting-Performance-Maven23` folder, or its `pom.xml`.
3. Trust the project and let IntelliJ import Maven dependencies (internet is required on first import).
4. Select **Project SDK: JDK 23** in Project Structure.
5. Open `src/main/java/sortbenchmark/Main.java` and click the green **Run** triangle beside `main`.
6. To run the JUnit tests, right-click `src/test/java/sortbenchmark/AlgorithmTests.java` → **Run**.

You do not need `run.bat`, `test.bat`, `run.sh` or `test.sh`.

## Run with Maven in PowerShell

In the folder containing `pom.xml`:

```powershell
mvn clean test
mvn clean package
java -jar target\java-sorting-performance-1.0.0.jar
```

- `mvn clean test` compiles and runs all JUnit tests.
- `mvn clean package` creates a runnable JAR with `sortbenchmark.Main` configured in its manifest.
- `java -jar ...` launches the graphical interface.

On the first build, Maven downloads build plugins and JUnit dependencies. After a successful download these are usually cached locally.

## Demonstration

1. In the application, click **Upload CSV**.
2. Choose `sample-data/students.csv` from the project folder.
3. Select the **English_Marks** numeric column.
4. Click **Compare 5 Algorithms**.
5. See the timing table, winner, and sorted rows.
6. Optionally click **Export Sorted CSV**.

CSV files must be UTF-8, have a header and consistent column counts. The selection box only offers columns where every data row contains a finite numeric value. The parser handles quoted commas, quoted newlines and escaped double quotes. Timings are measured using `System.nanoTime()` over five measured runs, excluding data copying; the median time determines the winner. Each algorithm receives the same original input and its result is checked against an independently sorted reference.

> Note: Exact execution timings depend on CPU load, file size and JVM warm-up. For files over 10,000 rows, Insertion Sort may be slow.

## Standard directory structure

```text
Java-Sorting-Performance-Maven23/
├── pom.xml
├── .gitignore
├── README.md
├── sample-data/
│   └── students.csv
└── src/
    ├── main/
    │   └── java/
    │       └── sortbenchmark/
    │           ├── Main.java
    │           ├── data/
    │           │   ├── CsvLoader.java
    │           │   ├── CsvDataset.java
    │           │   └── CsvExporter.java
    │           ├── ui/
    │           │   └── SortingAppFrame.java
    │           ├── algorithms/
    │           │   ├── SortAlgorithm.java
    │           │   ├── InsertionSort.java
    │           │   ├── ShellSort.java
    │           │   ├── MergeSort.java
    │           │   ├── QuickSort.java
    │           │   └── HeapSort.java
    │           ├── benchmark/
    │           │   ├── PerformanceEvaluator.java
    │           │   ├── BenchmarkReport.java
    │           │   └── AlgorithmResult.java
    │           └── model/
    │               └── SortItem.java
    └── test/
        └── java/
            └── sortbenchmark/
                └── AlgorithmTests.java
```

