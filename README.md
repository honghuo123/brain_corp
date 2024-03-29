Installation
====

Implemented as a Java servlet, the application can be run in any J2EE container with Java 8. Installation can be done by simply dropping the WAR file into the webapps directory.

Configuration
====

Configuration is done by modifying web.xml

 • passwd_path: file path for passwd file. Default /etc/passwd

 • group_path: file path for group file. Default /etc/group

 • refresh_time: interval between file refreshes. Default 1 second
 
Unit-tests
====

Unit-tests were done by shell scripts corresponding directly to the use cases, since methods have 1:1 mapping, and scripts covers end-to-end as well. For more complex cases I would use JUnit.

Future considerations
====

Further enhancements can be made in the following areas, once business needs can be clearly established

• File integrity checks. Current code checks field numbers of each row, and throws exceptions when errors are found. More granular checks, like data types and length of each field, can be implemented as needed.

• File sync. Under Linux there's no real way to lock passwd and group files from other processes, thus racing condition can not be fully prevented. In real-life project, a synchronization method needs to be used, instead of using periodical checks

• JSON queries. Depending on actual size and percentage of query types, using JSON query libraries like JSONPath, may increase performance and reduce code maintenance costs. If performance is key concern, benchmark for different libraries should be conducted to make a final choice. For demonstration purpose simple full table scans were used in the this exercise

• Multi-thread performance. Current implementation allows as many concurrent HTTP threads to be run, and separate read/write locking mechanism allows optimal performance. Further tuning, however, can still be done using load testers like JMeter.

• System stability. Current code was put under 24-hour continues load, no memory leak was found. For real-life use, more rigorous test conditions need to be applied

• Unit-tests. More negative test-cases could be added. (I did cover some in my scripts, but for cleanness I didn't include all)
