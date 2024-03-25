# MapReduce Project

## Introduction

This project entails the development of a MapReduce framework tailored for a word counting task. The objective is to implement a master server responsible for orchestrating a set of workers, delegating various tasks, and aggregating results. The entire implementation must be carried out in C/C++.

### Task Description

**Word Count Task:** Given a collection of documents, the objective is to generate a key-value output containing the counts for each word. The resultant output file should be sorted by count, adhering to the format `keycount\n`.

The project involves processing large text files, where each line is read sequentially. Non-Latin symbols are to be ignored, and all text should be converted to lowercase. Participants are expected to craft their own map and reduce functions for this purpose.

## MapReduce Framework

For details on the MapReduce framework, please refer to the class notes and the seminal [MapReduce paper](https://research.google/pubs/pub62/). The implementation requires the following components:

- A master node responsible for coordinating tasks across multiple worker nodes.
- Support for the following command-line interface:

```
./mapreduce --input <inputdir> --output <outputdir> --nworkers <nWorkers> --nreduce <nReduce>
```

This command initiates a master node along with worker processes, executing MapReduce operations on files from `inputdir` and storing results in `outputdir`.

### Stages

1. **Map (Worker):** Generating intermediate files by processing input files.
2. **Reduce (Worker):** Aggregating values from the map stage and saving the results.
3. **Merge (Master):** Combining output from all reducers into a single sorted output file, `output.txt`.

### Requirements

- Implement workers utilizing RPC libraries, multithreading, or communication over sockets.
- Ensure that the next stage doesn't commence until the previous one concludes.
- The master node must effectively manage worker statuses and task assignments.

### File Handling

- Intermediate files should be named with prefixes denoting their map and reduce task numbers (e.g., `map.part-0-0.txt`).
- Result files from reduce tasks should be named `reduce.part-X.txt`.
- All files, including map, reduce, and merge outputs, are to be stored in `outputdir`.
