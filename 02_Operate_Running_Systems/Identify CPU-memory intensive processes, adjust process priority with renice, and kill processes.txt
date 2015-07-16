Identify CPU/memory intensive processes, adjust process priority with renice, and kill processes

Commands to identify running processes:
# top
# ps -ef
# ps -waux

Kill process:
# kill <PID>

Forcefully kill process:
# kill -9 <PID>

Alter priority of running process:
# renice <priority> <PID>

Alter multiple priorities at once:

# renice <priority> <PID> -u <username> -p <another_PID