# Template

Template

## ToDo and README

> [!IMPORTANT]
> Please, read carefully the READMEs and ToDos in root project, frontend and backend.
> These contain important instructions, troubleshooting steps, and an overview of the project's features.

## Main branch

The `main` branch should be a functional version of the project, in terms of basic features and,
more over, project structure. This means that the main branch should always be deployable
and functional, no matter what development stage the project is.

## Installation

### Prerequisites

Ensure you have the following software installed:
#### Global Requirements
- [Docker](https://docs.docker.com/get-docker/)
- [VSCode DevContainers Extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)
#### Windows-Specific Requirements
- [WSL2](https://learn.microsoft.com/en-us/windows/wsl/install)

### Setup Instructions

1. **Clone the Repository**: Start by cloning the project repository.

> [!CAUTION]
> #### Windows
> If you are using Windows, there is a known bug where DevContainers' host-mounted
> volumes won't be able to read Linux's Inotify filesystem events, therefore not updating
> files correctly. It's **highly advisable** to clone the repository directly inside **WSL2**.
>
> To do this, simply follow the instructions but using a WSL shell. To open a WSL shell,
> just execute the following in a CMD:
> ```bash
> wsl
> ```
> We recommend using a WSL distribution such as Ubuntu or Debian,
> which includes essential development tools like git.
> Otherwise, you will need to set up your environment accordingly.

> [!WARNING]
> #### MacOS
> MacOS platform hasn't been tested yet, thus unknown behavior is to be expected.
>
> Since macOS does not support WSL and uses `fswatch` instead of `inotify`,
> no workaround for potential issues has been proposed yet.

Use this to clone the repo.
   ```bash
   git clone https://github.com/IES-Las-Galletas-DAW-2025-Grupo-D/Proyecto-Final.git
   ```

## Workflow

To develope in this project, we make use of VSCode DevContainers extension.

### Enter a developing environment

Once the cloned project is opened using `code .`, you can access frontend or
backend developing environments by opening the command palette (`CTRL+SHIFT+P`
in windows by default) and running `>Dev Containers: Reopen in Container`.

This will reopen VSCode in the selected DevContainer. Needed extensions and
dependecies will be installed.
> [!NOTE]
> Note that the project containers (services) will be composed.
> You can manage these using Docker Desktop (they should appear there).

> [!NOTE]
> Note that one of these containers (frontend or backend) is also the DevContainer
> you are using. This means we develop in the same evnironment we deploy services.
> And everyone uses the same dependecies and VSCode extensions. Therefore is not
> recommended to install additional extensions, if these require to be installed in
> the DevContainer.

### Switch to a different developing environment

If you want to switch from backend to frontend environment, and vice versa, you can use
the command (command palette) `>Dev Containers. Switch Container`. That easy!

> [!TIP]
> You can have both backend and frontend environments opened at once. To do this,
> simply open a new VSCode (command palette) `>New Window`, and then do the normal
> steps you'd do to open the cloned project and a DevContainer.

### Return to the root folder

Even tho each DevContainer contains the entire code base, it's common to want to exit
a DevContainer and have a view of the root project (not in developing environment).

To do this, there are two ways. You could use the command (command palette)
`>Dev Containers: Reopen Folder Locally`. The downside of using this is that is not
fully compatible with WSL environment. This means that, when executed, it'll attempt
to open the cloned project but in native Windows Filesystemt. So you will have to
manually open it again using WSL. For that reason, we prefer to open it directly
using the command (command palette) `>File: Open Recent...`.

> [!TIP]
> If you feel lost, remember that you can always open again WSL and manually navigate
> to the project folder (where you cloned it) and execute `code .`.

## Troubleshooting

- **Docker Issues**: If you encounter any issues with Docker and port bindings, try the following:

  1. **Port Already in Use**: Check if the required ports (3000, 8000, 3306) are already in use.
     ```cmd
     netstat -aon | findstr "3000 8000 3306"
     ```
     Kill the processes using the ports (replace `PID` with the actual process ID).
     ```cmd
     taskkill /F /PID [PID]
     ```
  2. **Reset WinNAT**: Try resetting the WinNAT network using privileged PowerShell.
     ```powershell
     net stop winnat
     net start winnat
     ```
     You can check the excluded port range of WinNAT, to make sure it was the issue.
     ```powershell
     netsh interface ipv4 show excludedPortRange protocol=tcp
     ```
     _Of course, Windows making trouble for no reason..._
