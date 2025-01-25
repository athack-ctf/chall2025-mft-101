# How to Solve the Challenge?

MFT stands for "Master File Table," which is a crucial file that stores information about every file and directory on a volume, including their location, size, creation date, and other metadata, essentially acting as a database to track all files on the drive; every file on an NTFS partition has at least one corresponding entry in the MFT. 

We have few questions to answer about the secret file. First, we need a tool that help us parse the MFT file to get as much info from it, there are several tools that can do the job but our go tool is `MFTECmd` by Eric Zimmerman (Zimmerman has a wide variation of tools to help DFIR people doing the job). We can find the list of the tools [here](https://ericzimmerman.github.io/#!index.md)
