Confirm the VM created in the previous lesson boots correctly and has sufficient CPU and memory assigned to it.
Open Git CLI and SSH into your local ubuntu server VM. You will do this via password authentication.

Q1: Why is password authentication inferior to public key authentication?

Find an online guide to setup public key authentication on your ubuntu vm.
Once complete, store the key in the folder C:\Users\YOUR_USER_NAME\.ssh
  I recommend storing the key with a name that is meaningful for you. eg server_name.ip_address.key
    eg prod-testing.192.168.0.1.key
Confirm using git CLI that you can connect using the key. You will need a specific command to add the identity file.
Reconfigure SSH server to no longer accept password authentication.
Confirm that passwords are no longer accepted.

VSCode will be your primary text editor for this course.

Q2: Why is VSCode a good choice for a text editor and how does it differ from a fully-fledged IDE?

Open VSCode, install the extension 'Remote - SSH' and connect to your VM using the ssh key.
  The SSH config file should be located in the same directory you placed the SSH key earlier.
  here is an example config entry
    Host prod-testing
    HostName 158.101.99.186
    User ubuntu
    IdentityFile ~/.ssh/test.key

Once connected, open the integrated VSCode terminal and clone your fork of this repository into the VM.
Use the VSCode File menu to 'open folder' at your cloned repository. You should now have complete access to the remote filesystem of your VM in the 'explorer' left hand menu of VSCode.

Q3: What is SCP over SSH and why is using VSCode remote SSH convenient for managing remote instances?
Q4: What is a git repository? What happens during a git clone? What do the terms 'remote' and 'origin' mean in this context?
Q5: What is the benefit of forking a repository and submitting pull requests vs sharing repository access and pushing directly to master?
Q6: Why are git branches useful? how would you organise a repository to best use branches?

Experiment with hyper-v by doing the following in any order:
  Save the state of your vm and restore it.
  Create a snapshot, make changes to the vm filesystem and then restore the snapshot.
  Shut down your VM and restart it.
  Forcefully terminate your VM.
  Export your VM, remove it from hyper-V and then re-import it.

Q7: Why is it important to frequently commit and push your changes to a remote repository (eg your forked repo on GitHub)?
Q8: Why are VM snapshots important?
Q9: When and why would you choose to use incremental backups vs full backups? 
Q10: What port is SSH usually exposed on? What are the security implications of having this port exposed to the internet? Is it worthwhile changing the port?
Q11: What could happen if your SSH key is compromised?
Q12: What are the security implications of using software that is no longer supported or has not been updated?
Q13: Explain these software terms: LTS, Stable, Alpha, Beta, RC
Q14: At a generalised level, how is open source software usually managed? What is an RFC?
Q15: What is a Unix socket and why can't multiple applications listen on the same port? Does this also apply to Windows?
Q16: What is a reverse proxy and how can it be used to allow multiple applications to listen on a single port?
Q17: What is NGINX and why is it considered preferable to Apache?
Q18: What is a page file? What happens to applications that exhaust all available system memory? Is 'paging' bad?
Q19: Why is dynamic memory, also known as memory ballooning, a useful technology for virtual machines?
Q20: What are processes? Can they share memory?
Q21: What are threads? Can they share memory?
Q22: What is CPU IPC and frequency? Why is CPU speed more important for single threaded applications than multi-threaded applications?
Q23: What is the difference between concurrent and parallel execution? What does 'thread safety' mean?
Q24: If a CPU has 4 cores, how many processes can it execute concurrently?
Q25: Explain the difference between synchronous and asynchronous code. When would you prefer one technique over the other?
Q26: Can a linux web-server operate acceptably with 1CPU and 512MB RAM? Can a Windows server do the same?
Q27: Is it bad for an operating system to have assigned all its available memory? When might this occur and why can it be beneficial to performance rather than detrimental?
Q28: What are the operational pros/cons of using a Linux server vs a Windows server?
Q29: What are the financial implications of using open source software vs propriety software? (Specifically regarding operating system and database choice)
Q30: Why would you want to avoid vendor lock-in at an operational level?
Q31: What is PCIE and NVME? What are storage IOPS? Explain the pros and cons of using NVME SSD's for production servers.
Q32: Explain the typical difference between standard type and archive type cloud storage? What technology is typically used for archival storage? What are the pros/cons for utilising archival storage?