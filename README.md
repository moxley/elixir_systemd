# Elixir Application as SystemD Service

These instructions show how to make systemd responsible for keeping an application running.
If the underlying machine reboots, the application will be automatically started as well.
If the application crashes, it will be automatically restarted.

These instructions assume the application is an Elixir application built with `mix release`,
but it can be adapted for other runtimes and situations. It assumes you've already
run `MIX_ENV=prod mix release`, which writes release files to `_build/prod/rel/...`.

## Installation

1. Copy the service unit file to the appropriate location:
   ```sh
   sudo cp my-app.service /etc/systemd/system/
   ```
2. Start the SystemD service and check its status:
   ```sh
   sudo systemctl start my-app
   systemctl status my-app
   ```
3. Enable the service:
   ```sh
   sudo systemctl enable my-app
   ```

If you make changes to the service unit file, copy it to `/etc/systemd/system/` again,
and tell SystemD to reload the changes:

```sh
sudo systemctl daemon-reload
```

## Logs

To view logs from the service, run this:

```sh
journalctl -f -u my-app
```
