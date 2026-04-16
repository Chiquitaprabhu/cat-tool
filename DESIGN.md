problem statement
Here we are building our own version of the Unix command line tool cat. The cat tool displays all the contents of the file and numbers them with the flags provided.
functional requirements
- Accepts multiple file path arguments and concatenates their contents in order.
- Supports flag -n  to output the contents of the file, will number it and consider the blanks
- Supports flag -b  to output the contents of the file, will number it and not consider the blanks
- When no flag is given, outputs the entire file
- Accepts input from a file path argument
- Accepts input from stdin when data is piped in
Error Handling:
- [invalid flad — will throw an error saying -  illegal option.]
- [missing file — will throw an error saying - No such file or directory.]
- [no arguments — wait for user to input]
non-functional requirements 
Memory : we will read one line at a time to not overwhelm our RAM.
Error Handling : The tool displays clean, user-friendly error messages for invalid flags and missing files. No Python tracebacks are shown to the user.

Data Flow Diagram:

sys.argv → [parse_flags()] → flags ,n*[file_path]
                                    ↓
                    file or stdin → [print_lines(source)] 
                                    ↓
                                  print output

structure

- parse_flags(): loops through sys.argv, separates flag and filename, validates flags against supported options (-n, -b).
- print_file(source, numbering_mode): will take in the mode as none, all, nonblank


- Main flow: 
1. Parse and validate arguments (exit early if invalid flag or nonexistent file)
2. Determine input source (file or stdin)
3. Call print_file with the source (catch FileNotFoundError)
4. Display results

design decisions
- Chose manual sys.argv parsing over argparse because the tool only has two flags. Manual parsing is simpler to implement and easier to read for a small number of arguments. For a tool with many flags or complex argument relationships, argparse would be the better choice. 

Testing
compare against head tool:
[1] empty file
[2] file with no new line
[3] nonexistent file
[4] test stdin input (piping) 
[5] cat -z motivation.txt
[6] cat -n motivation.txt
[6] cat -b motivation.txt
[7] Multiple files with no flag
[8] Multiple files with -n - numbering doesn't continue across files
[9] One real file + one nonexistent file 
[10] cat


