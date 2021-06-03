Confirm the VM created in the previous lesson boots correctly and has sufficient CPU and memory assigned to it.
Open Git CLI and SSH into your local ubuntu server VM. You will do this via password authentication.

Q1: Why is password authentication inferior to public key authentication?

Because Key based authentication is computer generated, rather than human generated, and typically 4096 Bits in length
less prone to being brute forced, acquired by subterfuge or guessed than a traditional password. 

Communications between two system using a key pair method is only possible to decrypted by owners of the key pair.
Furthermore a private key can typically be further encrypted with a standard password to increase safety.


Find an online guide to setup public key authentication on your ubuntu vm.
Once complete, store the key in the folder C:\Users\YOUR_USER_NAME\.ssh
  I recommend storing the key with a name that is meaningful for you. eg server_name.ip_address.key
    eg prod-testing.192.168.0.1.key
Confirm using git CLI that you can connect using the key. You will need a specific command to add the identity file.
Reconfigure SSH server to no longer accept password authentication.
Confirm that passwords are no longer accepted.

VSCode will be your primary text editor for this course.

Q2: Why is VSCode a good choice for a text editor and how does it differ from a fully-fledged IDE?

Visual Studio and other IDEs are intended as entire application or project construction platforms, whereas VSCode is a
more of a build and debug text editor. It lacks some functionality that VS has however it is fast, and well designed 
for cloud applications.

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

Secure Copy Protocol is a file transfer method that uses the Secure Shell protocol. particularly useful when performing client to remote or remote to remote file transfers.
Using VSCode gives you the added functionality of behaving like a GUI, to navigate through files and edit code on the remote instance.

SCP is considered an outdated connection method since overshadowed by Rsync and SFTP.

Q4: What is a git repository? What happens during a git clone? What do the terms 'remote' and 'origin' mean in this context?

A git repository is a essentially a version control system that allows multiple developers to work simultaneously on source code and effectively allows for updates, merging, compare and other similar functions like cloning and forking to provide
developers with the tools they need to work collaboratively. 

Cloning simply copies the repository from its remote source to a location locally. Becoming standalone in the process and disconnected from the source content.

The remote in this instance is the location that is a copy of the original branch, whereas the origin is the centralsied point from which the most up to date version of a project would be distributed from.

Q5: What is the benefit of forking a repository and submitting pull requests vs sharing repository access and pushing directly to master?

I believe this is because its far safer for you to have your own copy, with which you can experiment freely with, and risk nothing other than your copy, then when you are satisfied that your work does not break anything or fail.
You can submit a pull request for the original author to view the changes before integrating them with the original source code. Protecting the project from potential errors.

Sharing repository access and pushing directly to the master could result in unforseen changes, potential for multiple changes from different users to conflict, and other such erroneous behaviour.

Q6: Why are git branches useful? how would you organise a repository to best use branches?

Branches are useful because it allows you to move the head and thus pointer to different instances of the work you are doing, enabling you to seperate out paths of changes, whether thats fixing mulitple seperate issues. Or coming up
with multiple solutions for the same problem, branching these allows you to pick and choose between them and merge the ones that are useful, and merge changes with the master branch.

To organise them I would simply create a branch for each change you wish to make, roughly speaking, so if you were to make a change to the code to solve a particular bug or functionality requirement then you would title that branch accordingly.

Allowing you to compare and merge those changes individually and check for issues that may arise or errors that are made before combining them into the master branch.


Experiment with hyper-v by doing the following in any order:
  Save the state of your vm and restore it.
  Create a snapshot, make changes to the vm filesystem and then restore the snapshot.
  Shut down your VM and restart it.
  Forcefully terminate your VM.
  Export your VM, remove it from hyper-V and then re-import it.

Q7: Why is it important to frequently commit and push your changes to a remote repository (eg your forked repo on GitHub)?

Frequent commit and push will safeguard your work against loss of data if the original is somehow compromised, as well as ensuring that with smaller consistent changes, anything that causes
a problem elsewhere or breaks something is easily identifiable, committing a lot of work at once increases the chance of a conflict with code that is submitted and will make it harder to
troubleshoot an error should one arise.

Q8: Why are VM snapshots important?

VM Snapshots when done regularly will allow you to restore a VM to a state much closer to that which it was before an error or failure occurs, saving lots of time and effort in lost work
Ultimately saving the state of the machine like this is similar to regularly saving your work, if it goes down and you have to restore it, you will have lost less if you snapshot regularly
restoring it to a state before it experienced a problem.

Q9: When and why would you choose to use incremental backups vs full backups? 

Incremental backups are especially useful when backing up large amounts of data or data that changes infrequently, by having the backup only transfer that which has changed since the
previous backup, you can save a lot of network traffic, data transfer costs.

Q10: What port is SSH usually exposed on? What are the security implications of having this port exposed to the internet? Is it worthwhile changing the port?

SSH is exposed on port 22 by default, the security implications are that an attacker would know where to look for the port making a connection atttempt, changing the port would likely make
the default operation of a lot of programs function incorrectly without additional configuration, such as any SSH connection would need to be told explicitly which port is listening for the SSH commands.

I would guess a determined attacker would scan all ports on a location for the port that responds to an SSH request if thats what they were looking for and perhaps the obfuscation of the SSH port would Ultimately
prove pointless because of this? Ultimately you might end up with less risk because bots set to attempt port 22 would miss it but ultimately if its configured correctly such an attack would be futile.

Q11: What could happen if your SSH key is compromised?

If your private SSH key is compromised, then forward secrecy should only allow that existing session to be compromised, and may allow someone to access the server, but not the remote.

Q12: What are the security implications of using software that is no longer supported or has not been updated?

New threats that are discovered and detected wont get patched for software that is unsupported or not been updated, making potentially fatal holes and exposing your system.

Q13: Explain these software terms: LTS, Stable, Alpha, Beta, RC

LTS - Long Term Support, meaning that the software or service on LTS is intended to be continued and updated, fixed and improved upon over the period of time they are in existence.
Stable - The current public mainstream working version of a software or service that is generally considered to be mostly bug free.
Alpha - Very premilinary stages of development, where much functionality is not complete and only specific elm


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