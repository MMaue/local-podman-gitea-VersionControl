### Local Version Control System podman gitea setup

If you want to have a local Version Control System, here's how you can set it up:

#### Step 1: Install WSL and a Linux Distribution

(only required if you're on Windows)  

1. **Enable WSL**: Open PowerShell or Windows Command Prompt as Administrator and run:
   ```powershell
   wsl --install
   ```
   This will enable the WSL feature and install the latest Ubuntu distribution by default. You can choose a different Linux distribution if you prefer. It will be located under: `C:\Users\{name}\AppData\Local\wsl\{id}`

2. **Set up Your Linux Distribution**: Launch the installed Linux distribution from the Start menu and follow the on-screen instructions to set up your username and password. (`wsl -d Ubuntu`)

#### Step 2: Install Podman

1. **Update Package Lists**: Open your WSL terminal and run:
   ```bash
   sudo apt update
   ```

2. **Install Podman**: Install Podman by running:
   ```bash
   sudo apt install -y podman
   ```

#### Step 3: Running Gitea with Podman

1. **Create a Volume for Gitea Data**:
   ```bash
   podman volume create gitea_data
   ```

2. **Run Gitea**:
   ```bash
   podman run -d --name gitea -p 3000:3000 -v gitea_data:/data docker.io/gitea/gitea:latest
   ```
   
   This command does the following:
    - `-d`: Runs the container in detached mode (in the background).
    - `--name gitea`: Names the container 'gitea'.
    - `-p 3000:3000`: Maps port 3000 of the container to port 3000 on your host machine.
    - `-v gitea_data:/data`: Mounts the `gitea_data` volume to the `/data` directory inside the container.
    - `docker.io/gitea/gitea:latest`: Pulls and runs the latest Gitea image from Docker Hub.

3. **Access Gitea**:
   - Open your web browser and navigate to `http://localhost:3000`.
   - Follow the on-screen instructions to set up Gitea.

4. **Start the Container**
  - `podman start gitea`

5. **Verify with**
  - `podman ps`
