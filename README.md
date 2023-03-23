# Pneumonia Detection using Chest X-ray Images and Convolutional Neural Networks
![cover](images/xray_cover.jpeg)

Overview
--------
This project involves developing a Convolutional Neural Network (CNN) from scratch using PyTorch to classify chest X-ray images as either normal or pneumonia. The CNN architecture comprises 6 convolution and max pooling layers, each with batch normalization and dropout regularization at 25% probability to prevent overfitting. Additionally, there are 6 fully connected layers, also with dropout regularization at 50% probability. The model has a little over 17 million trainable parameters. The dataset is imbalanced, with the normal class comprising 1349 images and the pneumonia class comprising 3883 images. To address this, a weighted loss function, BCEwithLogitsLoss, was employed. The model was trained with the help of DataLoaders in batches of 32 images, and the Adam optimizer. The primary performance metric used was accuracy. After training for 5 epochs on Colab's GPU accelerated environment, the model achieved a training accuracy of nearly 97% and a test accuracy of 81.41%. However, it became apparent that the model was overfitting and that a change in model architecture and hyperparameter tuning may be necessary. Currently the model is still under development.

Table of Contents
-----------------
1. Primary Objective
2. Results
3. Usage
4. Setup
5. Contributing
6. Credits
7. License
8. Contact

Primary Objective
-----------------
The primary objective of the project is to develop a Convolutional Neural Network (CNN) that can accurately classify chest X-ray images as "normal" or "pneumonia." The model's performance will be evaluated using metrics such as accuracy, precision, recall, and F1 score.

Results
-------
After training for 5 epochs on Colab's GPU accelerated environment, the model achieved a training accuracy of nearly 97% and a test accuracy of 81.41%. However, it became apparent that the model was overfitting and that a change in model architecture and additional hyperparameter tuning may be necessary.

Usage
-----
The model is currently under development with efforts to reduce the adverse effects of overfitting on the training data, and as a result it is not available for use at the moment. The optimized model will be made available in the future for use in medical diagnosis.

Setup
-----
**prerequisites**
- Google account
- GitHub account
- Git Bash (for Windows)
- Basic understanding of Git and GitHub

If you would like to train a CNN yourself, I recommend [Google Colab](https://colab.research.google.com/). This section provides step by step instructions for establishing connection with GitHub using SSH protocol.
<br><br>
Why is this necessary?<br>Training Deep Learning models are computationally intensive, consequently people utilize GPUs in addition to CPUs for faster execution of the task. If you do not have household GPUs, you can make use of resources provided by cloud services like Google Colab, AWS, Azure or others. That said, there are limitations to the usage of these resources. You can find out more about Google Colab through the link provided above.
<br>
<br>
Let's kick things off by briefly describing the procedure.
The Idea is to setup local repository on your Google Drive, mount the Google Drive on Colab and then use SSH protocol to interact with a remote repository (GitHub).
To do this you need a Secure Shell (SSH) key pair. This key pair has a public and a private key. The key pair can be generated using Git Bash (for Windows) or Terminal (Mac or Linux) or even on Google Colab's code cells with a '!' sign preceeding commands. The private key is then stored on your Google Drive and the public key on GitHub. The next step is to add the private key to an SSH agent. SSH agents provide a secure and efficient way to manage and use SSH keys for remote authentication.

1. **Generating SSH key pair**<br>
On your computer open Git Bash or Terminal and then type the following command.<br>
`ssh-keygen -t rsa -b 4096 -C "email@example.com"` and press Enter.<br>
The default location to save the key is in your user directory in .ssh folder and it will be called 'id_rsa', for example `/Users/shrey/.ssh/id_rsa`, you can leave it as it is or change 'id_rsa' to 'colabkey', for example: `/Users/shrey/.ssh/colabkey` (Note: This demonstration uses the name 'colabkey'). In the next substep you can optionally enter a pass phrase for your key or leave it blank (I left it blank). Once you are ready press enter. The key pair is generated and stored in the location specified above. If the key pair is not located in the specified folder, you can search and locate it or repeat the steps by specifying the full path when prompted, for example `/c/Users/shrey/.ssh/colabkey`.
2. **Accessing the keys**<br>
Navigate to the .ssh folder and you should find 'colabkey' and 'colabkey.pub' files. Next type this command<br>
`cat colabkey.pub`. This is will display a long string of characters and numbers. It starts with ssh-rsa and ends with your email. This is your public key and can be shared with others while the 'colabkey' file in this folder is your private key and should be securely kept on your local machine/storage. Copy your public key by highlighting the string.
3. **Adding the public key to GitHub**<br>
On GitHub, go to 'settings' and then go to 'SSH and GPG keys', click on 'New SSH key', give a title for example 'colabkey' and then paste your key in the 'Key' box. Click 'Add SSH key' and confirm with your GitHub password. That's it you have successfully added your public key to GitHub.
4. **Create a New repository on GitHub**<br>
Create a new repository on your GitHub profile, Give a relevant name for the repository (example: Pneumonia-detection-using-chest-X-ray-images-and-Convolutional-Neural-Networks), but do not add any files yet, be it README.md, LICENSE or .gitignore. This will complicate the process of establishing connection a bit.
5. **Moving the private key to Google Drive**<br>
- With the help of a file explorer copy the 'colabkey' or both 'colabkey' and 'colabkey.pub' files. 
- Go to your Google Drive and create a new folder called 'ssh_keys' in 'My Drive'. 
- Paste the files here.
- Create a 'config' file in the same folder and include the following content.<br>
```
  #colab account
  Host github.com
    HostName github.com
    User git
    IdentityFile /root/.ssh/colabkey
```
6. **Mounting your Google Drive on Colab**<br>
- On your Google Drive select or create a folder where you want to build more projects like this. You could perhaps name it 'colab_projects' or 'ColabProjects'.
- Create a new folder inside 'colab_projects' and name it exactly the same as the GitHub repository's name to which you want to connect. In this case 'Pneumonia-detection-using-chest-X-ray-images-and-Convolutional-Neural-Networks'. Please note that Git repository(s) will be created here; the .git folder will be placed inside 'Pneumonia-detection-using-chest-X-ray-images-and-Convolutional-Neural-Networks' and likewise for other projects.
- Please note that the code snippets below can be written on cells of Colab notebook incase you do not have access to the terminal provided for Colab Pro users. Include '!' before the commands if you're using cells to execute the command.
```
from google.colab import drive
drive.mount('/content/drive')
```
7. **Copying the Key(s) to Virtual Machine**<br>
Google Colab uses a Virtual Machine (VM) to provide computing resources for your notebook. We need to move the private key and config file to the Virtual Machine in order to facilitate communication with GitHub. When the runtime is disconnected these files will be erased from the Virtual Machine. The private key facilitates a mathematical proof that only this key could have generated the public key added to GitHub. 
```
# ssh keys were generated earlier. Private and Public keys are stored in 
# 'colabkey' and 'colabkey.pub' files. Additionally a config file is also 
# stored in /content/drive/MyDrive/ssh_keys/ on google drive.

# Remove ssh folder and its contents if already present
!rm -rf /root/.ssh

# Create a directory
!mkdir /root/.ssh

# Copy everything (ssh_key files & config file) from google drive to Virtual Machine.  
!cp /content/drive/MyDrive/ssh_keys/* /root/.ssh

# Set permission
!chmod 700 /root/.ssh 
```
8. **Adding GitHub as known host**<br>
```
# Add the git server as an ssh known host
!touch /root/.ssh/known_hosts

# Trust github  
!ssh-keyscan github.com >> /root/.ssh/known_hosts

# Set permission  
!chmod 644 /root/.ssh/known_hosts 
```
9. **Run an SSH-agent**<br>
```
# Run ssh-agent and add `ssh-add /root/.ssh/colabkey` in the prompt. 
# After this command, optinally check if the key is saved using `ssh-add -l`, 
# then exit the prompt.
!ssh-agent /bin/bash
```
10. **Check Connection with GitHub**<br>
```
!ssh -T git@github.com
```
You may get a message like this: "Warning: Permanently added the ECDSA host key for IP address '**.**.***.***' to the list of known hosts.
Hi user-name! You've successfully authenticated, but GitHub does not provide shell access."<br>

11. **Navigate to the project folder**<br>
for example:
```
cd drive/MyDrive/ColabProjects/Pneumonia-detection-using-chest-X-ray-images-and-Convolutional-Neural-Networks
```
confirm using `!ls` command in the next cell.<br>

12. **Initialize git repository**<br>
```
!git init
```
```
# Configure user name and email (if not already)
!git config user.name "shre-db"
!git config user.email "shreyasdb99@gmail.com"
```
```
# Check Staging Area
!git status
```
Go to the GitHub repository. In Quick setup section, You have the options to set up in desktop, use HTTPS or SSH. Select SSH and copy the url. for example `git@github.com:shre-db/Pneumonia-detection-using-chest-X-ray-images-and-Convolutional-Neural-Networks.git`. This URL specifies the location of a Git repository hosted on GitHub using the SSH protocol and will be used to add remote origin as shown below. In the code snippet below replace `git@github.com:shre-db/Pneumonia-detection-using-chest-X-ray-images-and-Convolutional-Neural-Networks.git` with the URL you've copied.
```
# Create README.md file Add files to the staging area, Commit the changes and Push
!echo "# Pneumonia-detection-using-chest-X-ray-images-and-Convolutional-Neural-Networks" >> README.md
!git add README.md notebook.ipynb
!git commit -m "Add README and notebook" -m "This commit includes a README file and a notebook containing code for preliminary setup."
!git branch -M main
!git remote add origin git@github.com:shre-db/Pneumonia-detection-using-chest-X-ray-images-and-Convolutional-Neural-Networks.git
!git push -u origin main
```

That's it you've successfully established an SSH connection with GitHub and can now interact directly from Colab notebook. After executing code snippets in step 12, you could consider commenting it out (cells in step 12 only) to avoid accidentally executing these cells again and as a result reinitializing the git repository the next time you run this notebook. You could dedicate a seperate set of notebook cells to run common commands to check status, add, commit, pull or push changes.

Contributing
------------
Thank you for your interest in this project! At this time we are not accepting contribution from external collaborators. If you have any feedback or suggestions, please feel free to create an issue or contact us directly.

Credits
-------
- Data:
  - Kermany, Daniel; Zhang, Kang; Goldbaum, Michael (2018), “Large Dataset of Labeled Optical Coherence Tomography (OCT) and Chest X-Ray Images”, Mendeley Data, V3, doi: 10.17632/rscbjbr9sj.3. Available at: https://data.mendeley.com/datasets/rscbjbr9sj/3
- I would like to thank [Dr. Mike X Cohen](https://www.mikexcohen.com/) for his guidance in designing and training Neural Networks. Please visit his [website](https://www.mikexcohen.com/) to find out more about him.
- I would like to thank ChatGPT, an OpenAI language model, and Bing for their invaluable assistance in providing general guidance for coding and troubleshooting errors throughout the development of this project.

License
-------
This project is licensed under the [MIT License](LICENSE) - see the [LICENSE](LICENSE) file for details.

Contact
-------
- **Name**: Shreyas
- **Email**: shreyasdb99@gmail.com
- **GitHub**: [shre-db](https://github.com/shre-db)
- **Instagram**: [shryzium](https://www.instagram.com/shryzium/)
