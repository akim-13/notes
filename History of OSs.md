---
tags:
  - cm12002
  - CS
links:
  - "[[Computer Systems Architectures]]"
  - "[[Operating Systems (OSs)]]"
  - "[[Computer History]]"
presentations:
  - W22_S3-4
---
# History of OSs
- At first, computers had **no [[./Operating Systems (OSs).md | OSs]] (*1960s*)**:
    - **No portability**, because everyone had to write code for the particular machine they were using.
    - Lots of **repeated code**.
    - Programmers **rarely saw the computer** themselves.

- A **job** is a combination of a program and its data.
    - Jobs were prepared on **paper tapes** or **punched cards**: 

        ![[Attachments/Pasted image 20240301192537.png]]
        ![[Attachments/Pasted image 20240301192601.png]]
        - The **punched card** encodes a single 80 character line (hence the 80 character limit on monitors later on).
        - The **paper tapes** had either 5 or 8 holes (hence 8 bits in a byte late on).

    - Jobs would be given to **operators** who would load and run them, collect the results and then send the results back to the programmer.
    - As computer time was limited, there was an issue of **[[Scheduling | scheduling]]** jobs, initially done by hand.

- **Spooling** is a process used in computing to manage data by holding it in a temporary storage area before it's processed.
    - In order for big and expensive computers to always run programs to minimized time wastage, spooling was utilized in the form of operators loading as many programs onto a fast medium, like a **magnetic tape**. The computer would load and run them as fast as hardware allowed.
    - Spooling would also be **used on output**: the output would be written to a magnetic tape, which could then later be attached to a printer (because printers are slower than computers).
    - This **addressed the disparity** between *human* and *computer* speeds.

- The process of loading programs from tape, running them and putting the results back on tape would soon be automated by a **job control language**.
    - A famous job control language from IBM was called **JCL**. 
    - The following is an **example of JCL code** that copies `OLDFILE` to `NEWFILE`:
        ```
        //IS198CPY JOB (IS198T30500),’COPY JOB’,CLASS=L,MSGCLASS=X
        //COPY01 EXEC PGM=IEBGENER
        //SYSPRINT DD SYSOUT=*
        //SYSUT1 DD DSN=OLDFILE,DISP=SHR
        //SYSUT2 DD DSN=NEWFILE,
        // DISP=(NEW,CATLG,DELETE),
        // SPACE=(CYL,(40,5),RLSE),
        // DCB=(LRECL=115,BLKSIZE=1150)
        //SYSIN DD DUMMY
        ```
        - This would be **set on 9 punched cards**.
    - JCL allowed for **batch processing** — the process of collecting and loading multiple programs in a single bunch. This is more efficient, because more time is spent running the programs and less time messing around in the overheads of loading and unloading.

- **Portable Batch System (PBS)** is a system designed for managing and scheduling batch jobs in networked computing environments.
    - PBS is **different from JCL** in that it allows for *dynamic scheduling* based on current workload and management of jobs *across various computing environments*, not just mainframe batch processing.

- The **monitor** is a program that automated the process of loading applications into memory (e.g. from tape), running and [./Scheduling.md | scheduling] them, i.e. **multitasking**. 

    ![[Attachments/Pasted image 20240301201453.png]]
    - It **utilised JCL**.
    - **When the application finished**, it would be expected to jump back to the monitor, so the monitor could deal with the next program.
    - The monitor **is not running while a program is running**, it only does its job when the program jumps back to it.
    - **Multitasking improves the efficiency** of use of a computer since while one program waits for a slow peripheral, another program can run.
    - However, there were several **problems**:
        1. Programs could accidentally or intentionally **corrupt each other or the monitor**.
        2. There was **no way to return control** to the monitor, e.g. in the case when a program goes into an infinite loop it can *bring down the entire system*.
