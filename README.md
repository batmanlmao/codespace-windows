# Codespace Windows

A minimal Windows 10 VM for GitHub Codespaces using [dockur/windows](https://github.com/dockur/windows).

## Start

```bash
docker compose -f compose.yml up -d
```

Then open forwarded port **8006** in the Codespaces **Ports** tab.

Watch the VM setup:

```bash
docker logs -f codespace-windows
```

## Stop / start

```bash
docker compose -f compose.yml stop
docker compose -f compose.yml start
```

Do **not** use `docker compose down -v` unless you intentionally want to remove persistent Docker volumes.

## Storage

- `./windows` contains the Windows VM disk and is ignored by Git.
- `./shared` is exposed inside Windows as the shared folder and is also ignored by Git.

Use the shared folder for files you want to move between the Windows VM and the Codespace.

## Why host networking?

GitHub Codespaces' normal Docker bridge networking can have DNS resolution problems. This setup uses host networking so the VM can use the Codespace host's working DNS path.

Because of host networking, there is no Docker `ports:` mapping in the compose file. Port 8006 is exposed directly by the container process and should be forwarded by Codespaces.

## N0va Desktop workflow

1. Start the Windows VM.
2. Open port 8006 and wait for Windows to finish installing.
3. Install/download N0va Desktop inside Windows.
4. Put the files you want to transfer into the Windows shared folder.
5. Access them from the Codespace under `./shared/`.
6. Download those files to your Android device.

Windows licensing is your responsibility.
