## Pipes and Redirection

A pipe is a form of redirection (transfer of standard output to some other destination) that is used in Linux and other Unix-like operating systems to send the output of one command/program/process to another command/program/process for further processing. The Unix/Linux systems allow stdout of a command to be connected to stdin of another command. You can make it do so by using the pipe character ‘|’.

`stdin, stdout, and stderr` are three data streams created when you launch a Linux command. You can use them to tell if your scripts are being piped or redirected

These are three standard streams that are established when a Linux command is executed. In computing, a stream is something that can transfer data. In the case of these streams, that data is text.

Data streams, like water streams, have two ends. They have a source and an outflow. Whichever Linux command you’re using provides one end of each stream. The other end is determined by the shell that launched the command. That end will be connected to the terminal window, connected to a pipe, or redirected to a file or other command, according to the command line that launched the command.

### The Linux Standard Streams

In Linux, stdin is the standard input stream. This accepts text as its input. Text output from the command to the shell is delivered via the stdout (standard out) stream. Error messages from the command are sent through the stderr (standard error) stream.

So you can see that there are two output streams, stdout and stderr, and one input stream, stdin. Because error messages and normal output each have their own conduit to carry them to the terminal window, they can be handled independently of one another.

### Streams Are Handled Like Files

Streams in Linux—like almost everything else—are treated as though they were files. You can read text from a file, and you can write text into a file. Both of these actions involve a stream of data. So the concept of handling a stream of data as a file isn’t that much of a stretch.

Each file associated with a process is allocated a unique number to identify it. This is known as the file descriptor. Whenever an action is required to be performed on a file, the file descriptor is used to identify the file.

These values are always used for `stdin, stdout, and stderr`:

   * 0: stdin
   * 1: stdout
   * 2: stderr


#### Code Examples
```bash
ls
#alien
#japanese.txt
#sentient.txt
#somefolder

ls | cat
# lists out the files in the directory
#alien
#japanese.txt
#sentient.txt
#somefolder

ls > files.txt
cat > files.txt
# creates a file with a list of the files in the directory
# alien
#files.txt
#japanese.txt
#sentient.txt
#somefolder

echo 'i am a file' > somefile.txt
cat somefile.txt
#i am a file

echo 'i am a another file eooo' >> somefile.txt
cat somefile.txt
#it appends/recreates the file
#i am a file
#i am a another file eooo

 ls -alh somesfsdfsdfsfds 2> err.txt
 cat err.txt
 # ls: cannot access 'somesfsdfsdfsfds': No such file or directory
```


### Filtering Output and Finding Things (&&, cut, sort, uniq, wc, grep)

* The AND Operator (&&) would execute the second command only, if the execution of first command SUCCEEDS, i.e., the exit status of the first command is 0. This command is very useful in checking the execution status of last command.

```bash
cat file1.txt && echo 'astonishing success'

# I am file1
# astonishing success
```


* This PIPE operator is very useful where the output of first command acts as an input to the second command. 

* The cut command in UNIX is a command for cutting out the sections from each line of files and writing the result to standard output. It can be used to cut parts of a line by byte position, character and field. Basically the cut command slices a line and extracts the text. It is necessary to specify option with command otherwise it gives error. If more than one file name is provided then data from each file is not precedes by its file name.

```bash
cut OPTION... [FILE]...

#For info on how to use
cut --help
```

* SORT command is used to sort a file, arranging the records in a particular order. By default, the sort command sorts file assuming the contents are ASCII. Using options in sort command, it can also be used to sort numerically.

```bash
cat mytext.txt | sort -bf
#sort the contents alphabetically

#Alek
#Bjorn
#Cattie
#Django
#Elon
#Freya
#Goro
```

* The uniq command in Linux is a command line utility that reports or filters out the repeated lines in a file.
In simple words, uniq is the tool that helps to detect the adjacent duplicate lines and also deletes the duplicate lines. uniq filters out the adjacent matching lines from the input file(that is required as an argument) and writes the filtered data to the output file .

```bash
cat alek.txt
#alek:we
#user:love
#someone:linux
#someone:linux

cat alek.txt | uniq
#alek:we
#user:love
#someone:linux
```

* wc stands for word count. As the name implies, it is mainly used for counting purpose. First column shows number of lines present in a file specified, second column shows number of words present in the file, third column shows number of characters present in file and fourth column itself is the file name which are given as argument.

```bash
cat new.txt
#abcd

wc new.txt
# 1 1 5 new.txt
```

* The grep filter searches a file for a particular pattern of characters, and displays all lines that contain that pattern. The pattern that is searched in the file is referred to as the regular expression (grep stands for globally search for regular expression and print out).

```bash
cat file.txt
#I am a new file

cat file.txt | grep new

#Searches all files in the directory for that keyword
grep someone ./*

#It gives us unique someones and cuts the first section before the delimiter -d
grep someone ./* | uniq | cut -d: -f1
```