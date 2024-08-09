<details>
  <summary>How debugger can access the private variables in Java?</summary>

In a JVM based on the OpenJDK codebase, a debugger uses a JVMTI agent to access the state of the program being debugged. The agent makes calls to the JVMTI native API. 
This allows agent (and hence the debugger) to read and write the values of object fields, local variables and so on. The JVMTI APIs ignore accessibility.
</details>
