
- Resource Monitor!!

**SysInternal Tools:**

- Sigcheck 
	- (make sure that this is installed - SysInternals tool and also ensure that the tools are in the EnvPATH in Windows)
	- Checking for Unsigned Files
		- `sigcheck -u -e C:\Windows\System32 -accepteula`

- Streams
	- `streams somefile.txt`
	- `notepad somefile.txt:ADS-NAME`
		- Where ADS-NAME is the additional stream name seen from running the streams program (additional stream to $DATA)
			- `:ads.txt:$DATA 26`

- Autoruns
	- anything weird in here? 

- ProcExp
- ProcMon

- PsExec ( go through this when you have more time : https://adamtheautomator.com/psexec/ )
	- When as admin
		- `psexec -s cmd`
			- Do a `whoami` after

- Winobj



**Command-line**

- `findstr`
	- Pattern matching utility
	- Example:
		- `strings portableexec.exe | findstr "remote"`