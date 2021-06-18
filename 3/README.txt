Task: Create a linux VM in Oracle Cloud accessible to the internet via HTTPS.

    Log into your Oracle Cloud account and create a compute instance (VM) with the following specification:
        Shape: VM.Standard.E2.1.Micro
        Memory: 1GB
        Cpu: 1vcpu
        Image: Canonical Ubuntu 20.04 minimal
    Save the private key and create the VM.
    Search how to detatch your current ipv4 address from the instance and replace it with a reserved (static) IP address.
        Make note of the static IP address.
    Search how to open port 443 in the security list of the vnic assigned to the instance.
    Move your private key to C:\Users\YOUR_USER_NAME\.ssh
        I recommend storing the key with a name that is meaningful for you. eg server_name.ip_address.key
    Connect via SSH using your IdentityFile
    Command: Update references to external packages
        sudo apt update
    Command: Install simple text editor
        sudo apt install nano -y
    Command: Create swap file
        sudo fallocate -l 3G /swapfile
        sudo chmod 600 /swapfile
        sudo mkswap /swapfile
        sudo swapon /swapfile
        echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab
        echo 'vm.swappiness=10' | sudo tee -a /etc/sysctl.conf
    Command: Allow access to HTTPS port 443
        sudo iptables -I INPUT 7 -m state --state NEW -p tcp --dport 443 -j ACCEPT
        sudo netfilter-persistent save
    Command: finish
        echo "setup complete"
        sudo reboot


Questions:
What will happen to your Oracle Cloud VM once your trial credits have expired?
Why would you want to use a static IP address vs a ephemeral address?
What is a vnic?
Why did we have to explicitly enable access to port 443 in the vnic security list?
Why did we have to explicitly enable access to port 443 inside the VM?
Why are we not exposing port 80 at either the vnic or the instance level? Why are we not simply exposing all ports?
Why did we need to run "apt update" before installing applications?
Why did we create a swap file for the instance?
What does chmod do? How are permissions managed on Linux?
What is a Linux superuser? What is the purpose of running commands as sudo?
Why must care be taken when executing commands as a superuser?
What is this command doing and why might it be useful for a Linux server instance? echo 'vm.swappiness=10' | sudo tee -a /etc/sysctl.conf


Task: Create a .net 5 rest api with JWT auth, swagger auto docs and an entity framework (ORM) data model.

    install vscode extensions
        https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csharp
        https://marketplace.visualstudio.com/items?itemName=Fudge.auto-using

    you will be creating a rest api inside the folder 3/todos-dotnet5-rest-jwt-ef-swagger
        your application name should be todos-dotnet5-rest-jwt-ef-swagger
        your application files should be placed directly inside 3/todos-dotnet5-rest-jwt-ef-swagger
    follow all three parts of this tutorial.
        https://dev.to/moe23/asp-net-core-5-rest-api-step-by-step-2mb6
    Compile and run your application via the dotnet cli
        https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-new
            build for debug: dotnet build
            run cross-platform binary: ./bin/Debug/net5.0/todos-dotnet5-rest-jwt-ef-swagger
        Vscode is able to forward listening ports from your remote instance to your local machine. you should be able to reach your application from localhost.
        You should be able to access the swagger documentation page for your app. try localhost/swagger or localhost/api/swagger
            You can use this page to manually test your API
    Test your implementation using the auto generated swagger documentation.
    Run your application with vscode debugger and trigger a breakpoint.
        If it's not working, check the configuration inside the .vscode folder provided as you may need to change the path to the application binary.
    Extend the api/todo endpoint with a new POST method called "seed"
        This method must generate 1,000,000 todos with unique data and save them to the database.
            The title field must be populated with a short random string. for example: "jFs'pX"
                Each title must contain 3 random lower-case characters.
                Each title must contain 2 random upper-case character.
                Each title must contain exactly 1 of the following special characters, at random
                    ! $ < > ( ) [ ] { } , " ' ` ; @ # / \ ©
                The order of all these characters must be random. for example:
                    jFs'pX
                    !spVrA
                    nHSv#w
            The description field must be populated with a series of two random words for a pool of words of your choosing. for example 'lorem ipsum'
            ~70% of the distribution of todos should be marked as complete. 
                This distribution must be random.
        The api must respond with a JSON object:
            {totalExecutionTime: 5246ms, completeTodos: 697,569, completedPercent: 69%}
                totalExecutionTime must be a string of this format: "{milliSeconds}ms".
                completeTodos must be a string representation (formatted with commas) of the number of completed todos created.
                completedPercent must be a string of the calculated percentage of completed todos created, formatted to 0 decimal places, with "%" appended.
    The swagger documentation page is configured to not be included in the release build. 
        Reconfigure it to be included in release. edit file "Startup.cs" and Search for env.IsDevelopment()
    Search how to 'publish' your application using dotnet cli
        You want to create a binary that runs without requiring dotnet to be installed in the host machine.
    Commit and push your changes (including the build) to your forked repo.
    SSH into your remote VM, pull your repo, launch the built binary and test your API using the instance's public IP address.


Questions:
What are database migrations?
Why are database migrations useful?
What would be the benefit of having both UP and DOWN migrations?
What is a JWT?
What are the pros and cons of JWT's vs sessions?
Where should JWT's be stored in the client browser?
What is the difference between authentication and authorisation?
Is a JWT sufficient enough to authorise a user?
How would you log out a user authenticated via JWT?
How would you revoke authorisation for a user authenticated via JWT?
Why would you want to implement a refresh token?
When would you use a GET request method?
When would you use a POST request method?
When would you use a PUT request method?
When would you use a DELETE request method?
Why are REST API's that only use GET and POST methods considered "Rest-like"? Why is this a common occurence?
Why is HTTP insecure and why should you always use HTTPS?
What are the benefits of automatic Swagger documentation?
What is the difference between an application binary and a generic binary file?
What is a dll?
Why must you ensure that production code is never released with a debug build?
Why is it important to profile your application for performance?
Why does developing/testing with a large seeded dataset allow you to spend less time profiling?
