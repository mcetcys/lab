
==================================================
PROGRAM 1: BINARIES, LIBRARIES AND MAKEFILE
(Original Question)
==================================================

AIM:
To study binaries, static libraries, dynamic libraries and Makefile.

PROCEDURE:
1. Create a C program.
2. Create a static library.
3. Create a shared library.
4. Compile and link the program.
5. Execute and verify the output.

PROGRAM:

File: hello.c

#include <stdio.h>

void hello()
{
    printf("Hello from Library\n");
}


File: main.c

void hello();

int main()
{
    hello();
    return 0;
}


Create static library:

gcc -c hello.c
ar rcs libhello.a hello.o
gcc main.c ./libhello.a -o static_app
./static_app


Create shared library:

gcc -fPIC -c hello.c
gcc -shared hello.o -o libhello.so
gcc main.c -L. -lhello -o dynamic_app
LD_LIBRARY_PATH=. ./dynamic_app


OUTPUT:

Hello from Library

RESULT:
Thus, static and dynamic libraries were successfully created and executed.


==================================================
PROGRAM 2: DAC IN LINUX
(Original Question)
==================================================

AIM:
To implement Discretionary Access Control in Linux.

PROCEDURE:
1. Create a file.
2. Create a user.
3. Change file ownership.
4. Set file permissions.
5. Verify the permissions.

PROGRAM:

sudo useradd user1

sudo touch sample.txt

sudo chown user1:user1 sample.txt

sudo chmod 640 sample.txt

ls -l sample.txt

OUTPUT:

-rw-r----- 1 user1 user1 0 sample.txt

RESULT:
Thus, DAC was successfully implemented using Linux file permissions.


==================================================
PROGRAM 3: DAC IN MYSQL
(Original Question)
==================================================

AIM:
To implement Discretionary Access Control in MySQL.

PROCEDURE:
1. Open MySQL.
2. Create a database.
3. Create a user.
4. Grant database permissions.
5. Verify and revoke permissions.

PROGRAM:

CREATE DATABASE college;

USE college;

CREATE TABLE student (
    id INT,
    name VARCHAR(30)
);

INSERT INTO student VALUES
(1, 'Arun');

CREATE USER 'user1'@'localhost'
IDENTIFIED BY 'pass123';

GRANT SELECT, INSERT
ON college.student
TO 'user1'@'localhost';

SHOW GRANTS FOR 'user1'@'localhost';

REVOKE INSERT
ON college.student
FROM 'user1'@'localhost';

SHOW GRANTS FOR 'user1'@'localhost';


OUTPUT:

Database created successfully.
Table created successfully.
User created successfully.
SELECT and INSERT permissions granted.
INSERT permission revoked.

RESULT:
Thus, DAC was successfully implemented in MySQL using GRANT and REVOKE.


==================================================
PROGRAM 4: RESUME WEB PAGE
(Original Question)
==================================================

AIM:
To create a personal resume webpage using HTML.

PROCEDURE:
1. Open a text editor.
2. Create an HTML file.
3. Add personal information.
4. Add education and skills.
5. Open the file in a browser.

PROGRAM:

<!DOCTYPE html>
<html>
<head>
<title>My Resume</title>
</head>

<body>

<h1>MY RESUME</h1>

<h2>Personal Details</h2>

<p>Name: Arun Kumar</p>
<p>Email: arun@gmail.com</p>
<p>Phone: 9876543210</p>

<h2>Education</h2>

<p>BE Computer Science</p>
<p>HSC - 2024</p>

<h2>Technical Skills</h2>

<ul>
<li>Python</li>
<li>Linux</li>
<li>HTML</li>
<li>Cyber Security</li>
</ul>

<h2>Experience</h2>

<p>Fresher</p>

</body>
</html>


OUTPUT:

A resume webpage is displayed containing:

Name: Arun Kumar
Email: arun@gmail.com
Education: BE Computer Science
Skills: Python, Linux, HTML, Cyber Security
Experience: Fresher

RESULT:
Thus, a personal resume webpage was successfully created.


==================================================
PROGRAM 5: LINUX VIRTUALIZATION USING CHROOT
(Original Question)
==================================================

AIM:
To implement Linux virtualization using the chroot mechanism.

PROCEDURE:
1. Create a root directory.
2. Create the required directories.
3. Copy the Bash shell.
4. Copy its required libraries.
5. Enter the isolated environment.

PROGRAM:

sudo mkdir -p /myroot/bin
sudo mkdir -p /myroot/lib
sudo mkdir -p /myroot/lib64

Copy Bash:

sudo cp /bin/bash /myroot/bin/

Check libraries:

ldd /bin/bash

Copy the required library files shown by ldd into their matching directories under /myroot.

Enter the environment:

sudo chroot /myroot /bin/bash

Execute:

echo "Welcome to Chroot"

pwd

exit


OUTPUT:

Welcome to Chroot
/

RESULT:
Thus, a basic isolated Linux environment was created using chroot.

NOTE:
Copy all dependencies reported by ldd. Chroot provides filesystem isolation, not complete virtualization.


==================================================
PROGRAM 6: MAC USING SELINUX / APPARMOR
(Original Question)
==================================================

AIM:
To implement Mandatory Access Control using AppArmor.

PROCEDURE:
1. Check AppArmor installation.
2. Check its service status.
3. Create an application profile.
4. Define file access permissions.
5. Enable enforce mode.

PROGRAM:

Check status:

sudo aa-status

Create profile:

sudo nano /etc/apparmor.d/usr.bin.testapp

Enter:

#include <tunables/global>

/usr/bin/testapp {
    #include <abstractions/base>

    /usr/bin/testapp mr,
    /etc/testapp.conf r,
    /tmp/testapp.log w,
}

Save the file.

Load profile:

sudo apparmor_parser -r /etc/apparmor.d/usr.bin.testapp

Enable enforcement:

sudo aa-enforce /etc/apparmor.d/usr.bin.testapp

Check:

sudo aa-status


OUTPUT:

AppArmor is loaded.
Profile is loaded.
Profile mode: enforce.

RESULT:
Thus, MAC was implemented using AppArmor security policies.


==================================================
PROGRAM 7: VIRTUAL PRIVATE DATABASE (ORACLE)
(Original Question)
==================================================

AIM:
To implement Virtual Private Database security using Oracle Label Security.

PROCEDURE:
1. Connect to Oracle.
2. Create an employee table.
3. Insert employee records.
4. Create security labels.
5. Apply security restrictions.

PROGRAM:

CREATE TABLE employee (
    id NUMBER,
    name VARCHAR2(30),
    department VARCHAR2(20)
);

INSERT INTO employee VALUES
(1, 'Arun', 'IT');

INSERT INTO employee VALUES
(2, 'Kumar', 'HR');

COMMIT;

Create a simple VPD policy function:

CREATE OR REPLACE FUNCTION dept_policy(
    schema_name VARCHAR2,
    table_name VARCHAR2
)
RETURN VARCHAR2
AS
BEGIN
    RETURN
    'department = SYS_CONTEXT(''USERENV'', ''CLIENT_IDENTIFIER'')';
END;
/

Add policy:

BEGIN
    DBMS_RLS.ADD_POLICY(
        object_schema => USER,
        object_name => 'EMPLOYEE',
        policy_name => 'DEPT_POLICY',
        function_schema => USER,
        policy_function => 'DEPT_POLICY',
        statement_types => 'SELECT'
    );
END;
/

Set department:

EXEC DBMS_SESSION.SET_IDENTIFIER('IT');

SELECT * FROM employee;


OUTPUT:

ID    NAME    DEPARTMENT
1     Arun    IT

RESULT:
Thus, department-based data access was restricted using Oracle VPD.

NOTE:
This program demonstrates Oracle VPD using DBMS_RLS, not Oracle Label Security. Oracle Label Security requires separate label and policy configuration.


==================================================
PROGRAM 8: MERKLE TREE AND ONE-TIME SIGNATURE
(Original Question)
==================================================

AIM:
To implement an authentication tree and one-time signature using Python.

PROCEDURE:
1. Import hashlib.
2. Create sample messages.
3. Generate message hashes.
4. Construct the Merkle tree.
5. Generate and verify a one-time signature.

PROGRAM:

import hashlib
import secrets

def H(data):
    return hashlib.sha256(data).digest()

# Merkle tree

messages = [
    b"Message1",
    b"Message2",
    b"Message3",
    b"Message4"
]

level = [H(m) for m in messages]

while len(level) > 1:
    level = [
        H(level[i] + level[i+1])
        for i in range(0, len(level), 2)
    ]

print("Merkle Root:", level[0].hex()[:16])

# Lamport signature

private = [
    [secrets.token_bytes(32) for _ in range(2)]
    for i in range(256)
]

public = [
    [H(x[0]), H(x[1])]
    for x in private
]

message = b"Hello"
digest = H(message)

signature = []

for i in range(256):
    bit = (digest[i//8] >> (7-i%8)) & 1
    signature.append(private[i][bit])

valid = True

for i in range(256):
    bit = (digest[i//8] >> (7-i%8)) & 1

    if H(signature[i]) != public[i][bit]:
        valid = False
        break

print("Signature Valid:", valid)


OUTPUT:

Merkle Root: (Hash value)
Signature Valid: True

RESULT:
Thus, a Merkle tree and Lamport one-time signature were implemented successfully.

NOTE:
A Lamport key must never be reused. Full Merkle authentication also requires authentication paths and verification against the root.


==================================================
PROGRAM 9: METASPLOIT FRAMEWORK
(Original Question)
==================================================

AIM:
To identify vulnerabilities using Metasploit in an authorized lab.

PROCEDURE:
1. Open Kali Linux.
2. Start Metasploit.
3. Search for auxiliary modules.
4. Select a scanner module.
5. Scan the authorized lab machine.

PROGRAM:

Start Metasploit:

msfconsole

Search:

search type:auxiliary name:ftp

Select scanner:

use auxiliary/scanner/ftp/ftp_version

Set target:

set RHOSTS 192.168.56.101

Execute:

run

View options:

show options


OUTPUT:

[*] Auxiliary module selected.
[*] Scanning target 192.168.56.101
[*] FTP service information received.
[*] Scan completed.

RESULT:
Thus, Metasploit was used to identify FTP service information in an authorized lab.

NOTE:
The output depends on the target and the availability of the FTP service.


==================================================
PROGRAM 10: SERVER LOG ANALYSIS
(Original Question)
==================================================

AIM:
To analyze server logs and identify suspicious activities using Python.

PROCEDURE:
1. Create sample server logs.
2. Read the log entries.
3. Identify failed login attempts.
4. Detect suspicious IP addresses.
5. Display the analysis result.

PROGRAM:

logs = [
    "192.168.1.10 GET /home 200",
    "192.168.1.20 POST /login 401",
    "192.168.1.20 POST /login 401",
    "192.168.1.20 POST /login 401",
    "192.168.1.30 GET /admin 403"
]

count = {}

for log in logs:

    data = log.split()

    ip = data[0]
    path = data[2]
    status = int(data[3])

    if path == "/login" and status == 401:
        count[ip] = count.get(ip, 0) + 1

    if status == 403:
        print("Suspicious IP:", ip)

for ip, value in count.items():

    print("IP:", ip)
    print("Failed Logins:", value)

    if value >= 3:
        print("Possible Brute Force Attack")


OUTPUT:

Suspicious IP: 192.168.1.30

IP: 192.168.1.20
Failed Logins: 3
Possible Brute Force Attack

RESULT:
Thus, suspicious activities were identified through server log analysis.


==================================================
PROGRAM 11: MULTIPLE SOURCE FILES AND SHARED LIBRARY
(APPLY-LEVEL QUESTION - PAGE 2)
==================================================

AIM:
To develop an application using multiple source files and a shared library.

PROCEDURE:
1. Create a header file.
2. Create a library source file.
3. Create a main source file.
4. Create a Makefile.
5. Compile and execute the application.

PROGRAM:

File: mathlib.h

int add(int a, int b);


File: mathlib.c

int add(int a, int b)
{
    return a + b;
}


File: main.c

#include <stdio.h>
#include "mathlib.h"

int main()
{
    int result = add(10, 20);

    printf("Sum = %d\n", result);

    return 0;
}


File: Makefile

all: main

libmath.so: mathlib.c mathlib.h
	gcc -fPIC -shared mathlib.c -o libmath.so

main: main.c libmath.so
	gcc main.c -L. -lmath -o main

clean:
	rm -f main libmath.so


COMMANDS:

make
LD_LIBRARY_PATH=. ./main


OUTPUT:

Sum = 30


RESULT:
Thus, multiple source files were compiled and linked using a shared library and Makefile.


==================================================
PROGRAM 12: DAC IN LINUX USING ACL
(APPLY-LEVEL QUESTION - PAGE 2)
==================================================

AIM:
To implement Linux DAC using file permissions and Access Control Lists.

PROCEDURE:
1. Create a shared directory.
2. Create two users.
3. Set directory ownership.
4. Give different ACL permissions.
5. Verify the permissions.

PROGRAM:

sudo useradd user1
sudo useradd user2

sudo mkdir /shared

sudo chown root:root /shared

sudo chmod 770 /shared

Create a file:

sudo touch /shared/data.txt

Give user1 read and write permission:

sudo setfacl -m u:user1:rw /shared/data.txt

Give user2 read permission:

sudo setfacl -m u:user2:r /shared/data.txt

Display permissions:

ls -l /shared/data.txt

getfacl /shared/data.txt


OUTPUT:

user::rw-
user:user1:rw-
user:user2:r--
group::---
other::---


RESULT:
Thus, different access permissions were successfully provided to multiple users using ACL.


==================================================
PROGRAM 13: MYSQL DAC WITH MULTIPLE USERS
(APPLY-LEVEL QUESTION - PAGE 2)
==================================================

AIM:
To create multiple MySQL users with different access permissions.

PROCEDURE:
1. Create a database.
2. Create a table.
3. Create two users.
4. Grant different permissions.
5. Verify user privileges.

PROGRAM:

CREATE DATABASE company;

USE company;

CREATE TABLE employee (
    id INT,
    name VARCHAR(30)
);

INSERT INTO employee VALUES
(1, 'Arun');

CREATE USER 'reader'@'localhost'
IDENTIFIED BY 'read123';

CREATE USER 'writer'@'localhost'
IDENTIFIED BY 'write123';

GRANT SELECT
ON company.employee
TO 'reader'@'localhost';

GRANT SELECT, INSERT
ON company.employee
TO 'writer'@'localhost';

SHOW GRANTS FOR 'reader'@'localhost';

SHOW GRANTS FOR 'writer'@'localhost';


OUTPUT:

Reader:
SELECT permission granted.

Writer:
SELECT and INSERT permissions granted.


RESULT:
Thus, multiple MySQL users were created with different access permissions.


==================================================
PROGRAM 14: RESUME WEBPAGE WITH TABLES AND LINKS
(APPLY-LEVEL QUESTION - PAGE 2)
==================================================

AIM:
To create a professional resume webpage using HTML and CSS with hyperlinks and tables.

PROCEDURE:
1. Create an HTML file.
2. Add personal details.
3. Create an education table.
4. Add technical skills.
5. Add hyperlinks and CSS formatting.

PROGRAM:

<!DOCTYPE html>
<html>

<head>
<title>Professional Resume</title>

<style>

body {
    font-family: Arial;
    background: #eeeeee;
    margin: 30px;
}

.container {
    background: white;
    padding: 20px;
    max-width: 700px;
    margin: auto;
}

h1, h2 {
    color: navy;
}

table {
    border-collapse: collapse;
    width: 100%;
}

td, th {
    border: 1px solid black;
    padding: 10px;
}

</style>
</head>

<body>

<div class="container">

<h1>ARUN KUMAR</h1>

<p>Email: arun@gmail.com</p>

<h2>Education</h2>

<table>

<tr>
<th>Course</th>
<th>Year</th>
</tr>

<tr>
<td>BE Computer Science</td>
<td>2024-2028</td>
</tr>

<tr>
<td>HSC</td>
<td>2024</td>
</tr>

</table>

<h2>Skills</h2>

<ul>
<li>Python</li>
<li>Linux</li>
<li>HTML</li>
</ul>

<h2>Portfolio</h2>

<a href="https://github.com/">GitHub</a>

</div>

</body>
</html>


OUTPUT:

Professional resume displayed with:
- Personal details
- Education table
- Technical skills
- GitHub hyperlink
- CSS formatting


RESULT:
Thus, a professional resume webpage was created using HTML and CSS.


==================================================
PROGRAM 15: CHROOT WITH REQUIRED DIRECTORIES AND LIBRARIES
(APPLY-LEVEL QUESTION - PAGE 2)
==================================================

AIM:
To create an isolated Linux environment using chroot.

PROCEDURE:
1. Create a root directory.
2. Create bin and library directories.
3. Copy Bash.
4. Copy required shared libraries.
5. Execute commands inside chroot.

PROGRAM:

sudo mkdir -p /jail/bin
sudo mkdir -p /jail/lib
sudo mkdir -p /jail/lib64

Copy Bash:

sudo cp /bin/bash /jail/bin/

Check dependencies:

ldd /bin/bash

Copy each required library shown by ldd into its corresponding directory under /jail.

Enter the environment:

sudo chroot /jail /bin/bash

Run:

echo "Inside Restricted Environment"

pwd

exit


OUTPUT:

Inside Restricted Environment
/


RESULT:
Thus, a restricted Linux filesystem environment was created using chroot.

NOTE:
All dynamic library dependencies must be copied. Additional device files and configuration may be needed for other applications.


==================================================
PROGRAM 16: APPARMOR WEB SERVER SECURITY
(APPLY-LEVEL QUESTION - PAGE 2)
==================================================

AIM:
To configure AppArmor to restrict a web server from accessing unauthorized files.

PROCEDURE:
1. Install AppArmor utilities.
2. Check AppArmor status.
3. Create a security profile.
4. Define allowed file access.
5. Enable enforce mode.

PROGRAM:

Install utilities:

sudo apt install apparmor-utils

Check status:

sudo aa-status

Create profile:

sudo nano /etc/apparmor.d/usr.sbin.testweb

Enter:

#include <tunables/global>

/usr/sbin/testweb {
    #include <abstractions/base>

    /usr/sbin/testweb mr,
    /var/www/html/** r,
    /var/log/testweb.log w,
}

Save the file.

Load profile:

sudo apparmor_parser -r /etc/apparmor.d/usr.sbin.testweb

Enable enforce mode:

sudo aa-enforce /etc/apparmor.d/usr.sbin.testweb

Check:

sudo aa-status


OUTPUT:

AppArmor profile loaded.
Profile mode: enforce.
Access outside the allowed paths is restricted.


RESULT:
Thus, AppArmor was configured to restrict unauthorized file access.

NOTE:
This is a sample profile for a hypothetical application. A real web server needs a profile matching its executable, libraries, logs and runtime paths.


==================================================
PROGRAM 17: ORACLE VPD WITH DEPARTMENT ACCESS
(APPLY-LEVEL QUESTION - PAGE 2)
==================================================

AIM:
To implement Oracle VPD using a security policy function.

PROCEDURE:
1. Create an employee table.
2. Insert department records.
3. Create a policy function.
4. Apply the VPD policy.
5. Test department-based access.

PROGRAM:

CREATE TABLE employees (
    id NUMBER,
    name VARCHAR2(30),
    department VARCHAR2(20)
);

INSERT INTO employees VALUES
(1, 'Arun', 'IT');

INSERT INTO employees VALUES
(2, 'Kumar', 'HR');

INSERT INTO employees VALUES
(3, 'Ravi', 'IT');

COMMIT;


Create policy function:

CREATE OR REPLACE FUNCTION emp_policy(
    schema_name VARCHAR2,
    table_name VARCHAR2
)
RETURN VARCHAR2
AS
BEGIN
    RETURN
    'department = SYS_CONTEXT(''USERENV'', ''CLIENT_IDENTIFIER'')';
END;
/


Add policy:

BEGIN
    DBMS_RLS.ADD_POLICY(
        object_schema => USER,
        object_name => 'EMPLOYEES',
        policy_name => 'EMP_POLICY',
        function_schema => USER,
        policy_function => 'EMP_POLICY',
        statement_types => 'SELECT'
    );
END;
/


Test IT:

EXEC DBMS_SESSION.SET_IDENTIFIER('IT');

SELECT * FROM employees;


OUTPUT:

ID    NAME    DEPARTMENT
1     Arun    IT
3     Ravi    IT


RESULT:
Thus, Oracle VPD restricted employee records according to the department identifier.


==================================================
PROGRAM 18: MERKLE TREE WITH AUTHENTICATION PATH
(APPLY-LEVEL QUESTION - PAGE 2)
==================================================

AIM:
To implement a Merkle tree and verify message integrity using an authentication path.

PROCEDURE:
1. Import hashlib.
2. Create four messages.
3. Calculate their hashes.
4. Construct the Merkle root.
5. Verify a selected message using its authentication path.

PROGRAM:

import hashlib

def H(data):
    return hashlib.sha256(data).digest()

messages = [
    b"Message1",
    b"Message2",
    b"Message3",
    b"Message4"
]

a, b, c, d = [H(x) for x in messages]

ab = H(a + b)
cd = H(c + d)

root = H(ab + cd)

# Authentication path for Message1
proof = [b, cd]

calculated = H(a + proof[0])
calculated = H(calculated + proof[1])

print("Merkle Root:", root.hex()[:16])

if calculated == root:
    print("Message Verified")
else:
    print("Verification Failed")


OUTPUT:

Merkle Root: (Hash value)
Message Verified


RESULT:
Thus, a Merkle authentication path was used to verify message integrity successfully.


==================================================
PROGRAM 19: METASPLOIT AUXILIARY AND EXPLOIT MODULES
(APPLY-LEVEL QUESTION - PAGE 2)
==================================================

AIM:
To demonstrate auxiliary and exploit modules in Metasploit using an authorized lab.

PROCEDURE:
1. Open Kali Linux.
2. Start Metasploit.
3. Search for auxiliary modules.
4. Run a service scanner.
5. Examine available exploit modules.
6. Select an exploit only for an intentionally vulnerable lab.
7. Validate the result.
8. Record the findings.

PROGRAM:

Start Metasploit:

msfconsole

Search auxiliary modules:

search type:auxiliary name:ftp

Select FTP scanner:

use auxiliary/scanner/ftp/ftp_version

Set lab IP:

set RHOSTS 192.168.56.101

Run:

run

Search exploit modules:

search type:exploit name:vsftpd

Display options:

show options

NOTE:
Do not execute an exploit unless the lab target and vulnerable service have been verified and authorized. This program demonstrates discovery and scanner use, not successful exploitation.


OUTPUT:

Auxiliary module selected.
FTP scanner executed.
Service information displayed.
Exploit search completed.


RESULT:
Thus, Metasploit auxiliary and exploit module discovery was demonstrated in an authorized environment.


==================================================
PROGRAM 20: SERVER LOG CLASSIFICATION AND CORRELATION
(APPLY-LEVEL QUESTION - PAGE 2)
==================================================

AIM:
To classify suspicious server log entries and identify possible security incidents.

PROCEDURE:
1. Create sample logs.
2. Read each log entry.
3. Identify HTTP error codes.
4. Count failed login attempts.
5. Display suspicious activities.

PROGRAM:

logs = [
    "10.0.0.1 GET /home 200",
    "10.0.0.2 POST /login 401",
    "10.0.0.2 POST /login 401",
    "10.0.0.2 POST /login 401",
    "10.0.0.3 GET /admin 403",
    "10.0.0.4 GET /home 200"
]

failed = {}

for log in logs:

    data = log.split()

    ip = data[0]
    path = data[2]
    status = int(data[3])

    if status == 401:
        failed[ip] = failed.get(ip, 0) + 1

    if status == 403:
        print("Forbidden Access:", ip)

print("Login Analysis:")

for ip, count in failed.items():

    print(ip, ":", count)

    if count >= 3:
        print("Possible Brute Force Attack")


OUTPUT:

Forbidden Access: 10.0.0.3

Login Analysis:

10.0.0.2 : 3

Possible Brute Force Attack


RESULT:
Thus, suspicious log entries were classified and possible attacks were identified.


==================================================
PROGRAM 21: MULTIPLE SOURCE FILES AND AUTOMATIC REBUILD
(APPLY-LEVEL QUESTION - PAGE 3)
==================================================

AIM:
To create a multi-file C application and automatically rebuild it using Makefile.

PROCEDURE:
1. Create a header file.
2. Create two C source files.
3. Create a Makefile.
4. Compile the program using make.
5. Modify a source file and rebuild.

PROGRAM:

File: calc.h

int add(int a, int b);


File: calc.c

#include "calc.h"

int add(int a, int b)
{
    return a + b;
}


File: main.c

#include <stdio.h>
#include "calc.h"

int main()
{
    printf("Sum = %d\n", add(5, 10));
    return 0;
}


File: Makefile

all: app

app: main.o calc.o
	gcc main.o calc.o -o app

main.o: main.c calc.h
	gcc -c main.c

calc.o: calc.c calc.h
	gcc -c calc.c

clean:
	rm -f app *.o


COMMANDS:

make
./app

Modify calc.c and run make again to rebuild.

OUTPUT:

Sum = 15

After modification and rebuilding, the updated program is executed.


RESULT:
Thus, a multi-file application was compiled and automatically rebuilt using Makefile.


==================================================
PROGRAM 22: DAC USING ACL FOR SHARED DIRECTORY
(APPLY-LEVEL QUESTION - PAGE 3)
==================================================

AIM:
To provide different access permissions to multiple users in a shared directory using ACL.

PROCEDURE:
1. Create two users.
2. Create a shared directory.
3. Create a file.
4. Assign different ACL permissions.
5. Verify the permissions.

PROGRAM:

sudo useradd user1
sudo useradd user2

sudo mkdir /shared

sudo chmod 770 /shared

sudo touch /shared/file.txt

Give user1 read and write access:

sudo setfacl -m u:user1:rw /shared/file.txt

Give user2 read-only access:

sudo setfacl -m u:user2:r /shared/file.txt

Display ACL:

getfacl /shared/file.txt


OUTPUT:

user::rw-
user:user1:rw-
user:user2:r--
group::---
other::---


RESULT:
Thus, multiple users were provided with different file access permissions using ACL.


==================================================
PROGRAM 23: MYSQL USERS WITH DIFFERENT PERMISSIONS
(APPLY-LEVEL QUESTION - PAGE 3)
==================================================

AIM:
To manage MySQL privileges and verify user access restrictions.

PROCEDURE:
1. Create a database.
2. Create a table.
3. Create two users.
4. Grant different permissions.
5. Verify access restrictions.

PROGRAM:

CREATE DATABASE company;

USE company;

CREATE TABLE employee (
    id INT,
    name VARCHAR(30)
);

INSERT INTO employee VALUES
(1, 'Arun');

CREATE USER 'reader'@'localhost'
IDENTIFIED BY 'read123';

CREATE USER 'admin1'@'localhost'
IDENTIFIED BY 'admin123';

GRANT SELECT
ON company.employee
TO 'reader'@'localhost';

GRANT ALL PRIVILEGES
ON company.employee
TO 'admin1'@'localhost';

SHOW GRANTS FOR 'reader'@'localhost';

SHOW GRANTS FOR 'admin1'@'localhost';


OUTPUT:

Reader:
SELECT permission only.

Admin1:
All table privileges granted.


RESULT:
Thus, MySQL users were created with different access permissions and restrictions.


==================================================
PROGRAM 24: RESUME WEBPAGE WITH PROFESSIONAL FORMATTING
(APPLY-LEVEL QUESTION - PAGE 3)
==================================================

AIM:
To modify a resume webpage using HTML and CSS with hyperlinks and tables.

PROCEDURE:
1. Create an HTML document.
2. Add personal information.
3. Add education details using a table.
4. Add technical skills.
5. Add hyperlinks and CSS styles.

PROGRAM:

<!DOCTYPE html>
<html>

<head>

<title>Resume</title>

<style>

body {
    font-family: Arial;
    background: #f0f0f0;
}

.container {
    background: white;
    width: 70%;
    margin: auto;
    padding: 20px;
}

h1 {
    color: navy;
}

table {
    width: 100%;
    border-collapse: collapse;
}

td, th {
    border: 1px solid black;
    padding: 8px;
}

</style>

</head>

<body>

<div class="container">

<h1>My Resume</h1>

<h2>Personal Details</h2>

<p>Name: Arun Kumar</p>
<p>Email: arun@gmail.com</p>

<h2>Education</h2>

<table>

<tr>
<th>Course</th>
<th>Year</th>
</tr>

<tr>
<td>BE</td>
<td>2024-2028</td>
</tr>

<tr>
<td>HSC</td>
<td>2024</td>
</tr>

</table>

<h2>Skills</h2>

<ul>
<li>Python</li>
<li>Linux</li>
<li>HTML and CSS</li>
</ul>

<h2>Links</h2>

<a href="https://github.com/">GitHub</a>

</div>

</body>
</html>


OUTPUT:

A professionally formatted resume webpage is displayed with tables, hyperlinks and CSS styles.


RESULT:
Thus, a professional resume webpage was successfully designed using HTML and CSS.


==================================================
PROGRAM 25: RESTRICTED LINUX ENVIRONMENT USING CHROOT
(APPLY-LEVEL QUESTION - PAGE 3)
==================================================

AIM:
To establish a restricted Linux environment using chroot.

PROCEDURE:
1. Create an isolated root directory.
2. Create bin and library directories.
3. Copy the required shell.
4. Copy shared library dependencies.
5. Execute commands inside chroot.

PROGRAM:

Create directories:

sudo mkdir -p /secure/bin
sudo mkdir -p /secure/lib
sudo mkdir -p /secure/lib64

Copy Bash:

sudo cp /bin/bash /secure/bin/

Check libraries:

ldd /bin/bash

Copy all listed shared libraries into their matching paths under /secure.

Enter environment:

sudo chroot /secure /bin/bash

Execute:

echo "Secure Environment"

pwd

exit


OUTPUT:

Secure Environment
/


RESULT:
Thus, a restricted Linux environment was established using chroot.

NOTE:
Chroot is not a replacement for containers or a complete security boundary.


==================================================
PROGRAM 26: SELINUX / APPARMOR WEB SERVER RESTRICTION
(APPLY-LEVEL QUESTION - PAGE 3)
==================================================

AIM:
To configure security policies to restrict a web server from accessing unauthorized files.

PROCEDURE:
1. Check AppArmor status.
2. Identify the web server profile.
3. Create or edit its security profile.
4. Define allowed directories.
5. Enable enforce mode.

PROGRAM:

Check status:

sudo aa-status

Check web server profile:

ls /etc/apparmor.d/

Create a sample profile:

sudo nano /etc/apparmor.d/usr.sbin.testweb

Enter:

#include <tunables/global>

/usr/sbin/testweb {
    #include <abstractions/base>

    /usr/sbin/testweb mr,
    /var/www/html/** r,
    /var/log/testweb.log w,
}

Load profile:

sudo apparmor_parser -r /etc/apparmor.d/usr.sbin.testweb

Enable enforcement:

sudo aa-enforce /etc/apparmor.d/usr.sbin.testweb

Check:

sudo aa-status


OUTPUT:

Profile loaded.
Profile mode: enforce.
Unauthorized access is restricted.


RESULT:
Thus, AppArmor security policies were used to restrict unauthorized web server file access.

NOTE:
This is a sample profile for a hypothetical executable. For Apache or Nginx, use and carefully modify the actual installed profile rather than replacing it with this sample.


==================================================
PROGRAM 27: ORACLE VPD WITH SECURITY POLICY
(APPLY-LEVEL QUESTION - PAGE 3)
==================================================

AIM:
To implement Oracle Virtual Private Database using a department-based security policy.

PROCEDURE:
1. Create an employee table.
2. Insert employee records.
3. Create a policy function.
4. Apply the VPD policy.
5. Verify department-based access.

PROGRAM:

CREATE TABLE employee (
    id NUMBER,
    name VARCHAR2(30),
    department VARCHAR2(20)
);

INSERT INTO employee VALUES
(1, 'Arun', 'IT');

INSERT INTO employee VALUES
(2, 'Kumar', 'HR');

INSERT INTO employee VALUES
(3, 'Ravi', 'IT');

COMMIT;


Create function:

CREATE OR REPLACE FUNCTION dept_security(
    schema_name VARCHAR2,
    table_name VARCHAR2
)
RETURN VARCHAR2
AS
BEGIN
    RETURN
    'department = SYS_CONTEXT(''USERENV'', ''CLIENT_IDENTIFIER'')';
END;
/


Add security policy:

BEGIN
    DBMS_RLS.ADD_POLICY(
        object_schema => USER,
        object_name => 'EMPLOYEE',
        policy_name => 'DEPT_SECURITY',
        function_schema => USER,
        policy_function => 'DEPT_SECURITY',
        statement_types => 'SELECT'
    );
END;
/


Set IT access:

EXEC DBMS_SESSION.SET_IDENTIFIER('IT');

SELECT * FROM employee;


OUTPUT:

ID    NAME    DEPARTMENT
1     Arun    IT
3     Ravi    IT


RESULT:
Thus, department-specific access was implemented using Oracle VPD.

NOTE:
The CLIENT_IDENTIFIER must be set by a trusted application after authenticating the user. It should not be freely controlled by untrusted users.


==================================================
PROGRAM 28: MERKLE TREE AND MESSAGE AUTHENTICATION
(APPLY-LEVEL QUESTION - PAGE 3)
==================================================

AIM:
To implement a Merkle authentication tree and verify message integrity.

PROCEDURE:
1. Import the hashlib module.
2. Create four messages.
3. Generate SHA-256 hashes.
4. Construct the Merkle tree.
5. Verify a message using its authentication path.

PROGRAM:

import hashlib

def hash_data(data):
    return hashlib.sha256(data).digest()

messages = [
    b"One",
    b"Two",
    b"Three",
    b"Four"
]

a = hash_data(messages[0])
b = hash_data(messages[1])
c = hash_data(messages[2])
d = hash_data(messages[3])

ab = hash_data(a + b)
cd = hash_data(c + d)

root = hash_data(ab + cd)

# Verify the first message

proof = [b, cd]

result = hash_data(a + proof[0])
result = hash_data(result + proof[1])

print("Merkle Root:", root.hex()[:16])

if result == root:
    print("Message Authentication Successful")
else:
    print("Authentication Failed")


OUTPUT:

Merkle Root: (Hash value)
Message Authentication Successful


RESULT:
Thus, the Merkle authentication tree successfully verified message integrity.


==================================================
PROGRAM 29: METASPLOIT AUXILIARY AND EXPLOIT MODULES
(APPLY-LEVEL QUESTION - PAGE 3)
==================================================

AIM:
To demonstrate auxiliary and exploit module usage in Metasploit.

PROCEDURE:
1. Open Kali Linux.
2. Start Metasploit.
3. Search auxiliary modules.
4. Run an authorized service scanner.
5. Search for exploit modules.
6. Examine module options.
7. Record scan information.
8. Prepare the vulnerability report.

PROGRAM:

Start Metasploit:

msfconsole

Search auxiliary modules:

search type:auxiliary

Search FTP scanner:

search type:auxiliary name:ftp

Select scanner:

use auxiliary/scanner/ftp/ftp_version

Set authorized target:

set RHOSTS 192.168.56.101

Run:

run

Search exploit modules:

search type:exploit name:ftp

Display options:

show options

Display information:

info


OUTPUT:

Metasploit started.
Auxiliary modules found.
FTP scanner selected.
Target scan completed.
Exploit modules listed.


RESULT:
Thus, Metasploit auxiliary and exploit module discovery was demonstrated in an authorized test environment.

NOTE:
An exploit should only be executed against an intentionally vulnerable target with explicit authorization.


==================================================
PROGRAM 30: SERVER LOG ANALYSIS USING FILTERING
(APPLY-LEVEL QUESTION - PAGE 3)
==================================================

AIM:
To classify suspicious server log entries using filtering and correlation techniques.

PROCEDURE:
1. Create sample server logs.
2. Read the log entries.
3. Filter HTTP error codes.
4. Count failed login attempts.
5. Identify suspicious IP addresses.

PROGRAM:

logs = [
    "192.168.1.1 GET /home 200",
    "192.168.1.2 POST /login 401",
    "192.168.1.2 POST /login 401",
    "192.168.1.2 POST /login 401",
    "192.168.1.3 GET /admin 403",
    "192.168.1.4 GET /home 200"
]

failed = {}

for log in logs:

    data = log.split()

    ip = data[0]
    method = data[1]
    path = data[2]
    status = int(data[3])

    if status == 401:
        failed[ip] = failed.get(ip, 0) + 1

    if status == 403:
        print("Suspicious Access:", ip)

print("\nFailed Login Analysis")

for ip, count in failed.items():

    print(ip, ":", count)

    if count >= 3:
        print("ALERT: Brute Force Attack Detected")


OUTPUT:

Suspicious Access: 192.168.1.3

Failed Login Analysis

192.168.1.2 : 3

ALERT: Brute Force Attack Detected


RESULT:
Thus, server logs were filtered and correlated to identify possible security incidents.


==================================================
END OF ALL 30 SYSTEM SECURITY LAB PROGRAMS
==================================================
