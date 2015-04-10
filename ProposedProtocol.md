# Proposed Protocol

### Commands

- STAGE *AXIOM_SET*
  - Success
    - Responds with : `XXX ok : staged`
    - Stages an in-memory axiom set for the current user session.
  - Failure
    - If the axiom set is not defined : `XXX Err : Unknown axiom set`.

- UNSTAGE *AXIOM_SET*
  - Success
    - Responds with : `XXX ok : unstaged`.
    - Unstages an in-memory axiom set.
  - Failure
    - If the axiom set is not defined : `XXX Err : Unknown axiom set`.

- REMOVE *AXIOM_SET*
  - Success
    - Responds with : `XXX ok : removed`.
    - Removes the axiom set from memory.
  - Failure
    - If the axiom set is not defined : `XXX Err : Unknown axiom set`.
    - If the axiom is staged : `XXX Err : Axiom is staged, please unstage it first`.


- DOWNLOAD *AXIOM_SET* (TO *ABSOLUTE_PATH*)
  - Success
    - Downloads `AXIOM_SET` to `ABSOLUTE_PATH` ( or stdout if no path is given ) and then responds with : `XXX ok : downloaded`
    - Removes the axiom set from memory.
  - Failure
    - If the axiom set is not defined : `XXX Err : Unknown axiom set`.
    - If the path is not absolute : `XXX Err : Relative path given.`.
    - If there's permission errors in writing files in `ABSOLUTE_PATH` : `XXX Err : Cannot write file in specified path.`.
  - **Notes**
    - The server doesn't understand the TO part. The server always writes to the connection and it's the client responsibility to handle output redirection and to remove the TO part before sending the command to the server.

- UPLOAD *ABSOLUTE_PATH* (AS *AXIOM_SET*)
  - Success
    - Shows a progress bar for the upload process.
    - Responds with : `XXX ok : uploaded`.
    - Uploads the axiom set with this absolute path to the server. The axiom set uploaded is not staged.
    - If the AS parameter is given the axiom sets get named with this name, otherwise the file name is used.
  - Failure
    - If the axiom set file is not accessible ( Ex. File not found or Permission Error ) : `XXX Err : Axiom set not found or not accessible`.
    - If the path is not absolute : `XXX Err : Relative path given.`.
    - `ADD` Command errors. Check the notes below.
  - **Notes**
    - The server doesn't understand this command. It's the client responsibility to convert this into an `ADD` command.

- ADD *AXIOM_SET_NAME* ... GO
  - Success
    - Responds with : `XXX ok : succeeded` on job success.
    - Same as `UPLOAD` but axioms are read from client instead of file.
    - `ADD *AXIOM_SET_NAME*` and `GO` both should be on a separate lines with zero or more lines between them.
  - Failure
    - If the axiom set name already exists : `XXX Err : Axiom set name already exists.`
    - If the axiom file given contains syntax errors : `XXX Err : Syntax error`.

- RUN (*JOB_NAME*) ... GO
  - Success
    - Prints the job's output and then responds with : `XXX ok : succeeded`.
    - Runs the job given.
    - If a name wasn't given, unnamed is used instead.
    - Axioms and theories added are only for the scope of this job.
    - `RUN (*JOB_NAME*)` and `GO` both should be on a separate lines with zero or more lines between them.
  - Failure
    - If the job given contains syntax errors : `XXX Err : Syntax error`.

- LIST
  - Success
    - Lists the in-memory axiom sets in the format `Staged : … \nUnstaged : … \n` or with `No axiom sets in memory.` each on a seprate line and then responds with responds with : `XXX ok : listed`.
  - Failure
    - Cannot Fail.

- HELP
  - Success
    - Prints a help message and then responds with : `XXX ok`.
  - Failure
    - Cannot Fail.

- QUIT
  - Success
    - Responds with : `XXX ok : Bye.`
    - The client get disconnected and the user's session gets cleaned.
  - Failure
    - Cannot Fail.

- *UNKNOWN_COMMAND*
  - Responds with : `XXX Err : Unknown command`

### Success Codes
WIP

### Error Codes
WIP

### Notes
- Transfer reliability is insured by TCP.
