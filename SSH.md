Thought for a couple of seconds


Here’s a super-quick guide to set up password-less SSH to **silver** (LIACS gateway) and then to **carbonite** via `ProxyJump`:

---

## 1. Make & load your key

```bash
# if you don’t have one already
ssh-keygen -t ed25519 -f ~/.ssh/id_ed25519 -C "you@example.com"

# start agent & add key
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519

# check it’s loaded
ssh-add -l
```

---

## 2. Send pub-key to silver

```bash
ssh-copy-id -i ~/.ssh/id_ed25519.pub your_user@ssh.liacs.nl
```

---

## 3. SSH config: silver

Edit `~/.ssh/config` and add:

```ssh-config
Host liacs
  HostName ssh.liacs.nl
  User your_user
  IdentityFile ~/.ssh/id_ed25519
  IdentitiesOnly yes
  ForwardAgent yes
```

---

## 4. Test silver

```bash
ssh liacs
```

No password? Good.

---

## 5. Send pub-key to carbonite

```bash
ssh-copy-id \
  -i ~/.ssh/id_ed25519.pub \
  -o ProxyJump=liacs \
  your_user@carbonite.liacs.nl
```

---

## 6. SSH config: carbonite

In `~/.ssh/config`, add:

```ssh-config
Host carbonite
  HostName carbonite.liacs.nl
  User your_user
  ProxyJump liacs
  IdentityFile ~/.ssh/id_ed25519
  IdentitiesOnly yes
```

---

## 7. Test carbonite

```bash
ssh carbonite
```

---

### Recap

1. Generate & load key
2. Copy key → silver
3. Config & test silver
4. Copy key → carbonite (with ProxyJump)
5. Config & test carbonite

Now `ssh liacs` and `ssh carbonite` won’t ask for a password.
