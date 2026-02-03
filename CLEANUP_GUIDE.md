# Disk Cleanup Guide

Your physical drive is running out of space. Follow these steps to free up storage.

## 1. Clean Up Unused Docker Images

Remove dangling and unused images that are taking up space:

```bash
# Remove unused images
docker image prune -a --force

# View all images before cleanup
docker images

# Remove specific image if needed
docker rmi <IMAGE_ID>
```

**Note:** This will delete all images not currently used by containers. Be careful if you have custom images.

---

## 2. Clean Up Stopped Containers

Remove stopped containers to free up space:

```bash
# Remove all stopped containers
docker container prune --force

# List all containers (including stopped ones)
docker ps -a

# Remove specific container if needed
docker rm <CONTAINER_ID>
```

---

## 3. Clean Up Docker Volumes (Orphaned)

Remove unused volumes:

```bash
# List all volumes
docker volume ls

# Remove unused volumes
docker volume prune --force
```

**Warning:** Only do this if you're sure volumes aren't needed. Your Nextcloud volumes should still be in use.

---

## 4. Check External Drive Space

Verify your external drive has adequate space for Nextcloud data:

```bash
# Check disk space on all drives
Get-Volume | Select-Object DriveLetter, FileSystemLabel, Size, SizeRemaining | Format-Table

# Check specific external drive storage
Get-Item "D:\" | ForEach-Object { "{0:N0} bytes / {1:N0} bytes" -f $_.usedspace, $_.totalspace }
```

---

## 5. Clean Docker Build Cache

Remove unused build cache to save significant space:

```bash
# Remove all unused build cache
docker builder prune --all --force
```

---

## 6. Monitor Nextcloud Logs for Issues

After cleanup, check if everything is still working:

```bash
# View Nextcloud container logs
docker logs nextcloud-aio-mastercontainer

# Follow logs in real-time
docker logs -f nextcloud-aio-mastercontainer
```

---

## 7. External Drive Maintenance (Optional)

If your host drive is full but external drive has space:

- Ensure external drive is properly mounted
- Verify Nextcloud data is actually using external drive storage
- Consider moving other non-critical data to external drive

---

## Recommended Cleanup Order

1. **Start here:** Clear unused Docker images (#1)
2. **Then:** Remove stopped containers (#2)
3. **Then:** Clean build cache (#3)
4. **Then:** Remove orphaned volumes (#4) - only if safe
5. **Finally:** Verify disk space (#5) and monitor logs (#6)

---

## Estimated Space Recovery

- **Unused images:** Can be 1-5+ GB
- **Stopped containers:** Typically 100s of MB
- **Build cache:** Can be 1-2+ GB
- **Total potential recovery:** 2-10+ GB depending on your setup

---

## Backup Warning

⚠️ **Before deleting anything:**
- Ensure your Nextcloud data on `/mnt/external_drive/nextcloud_storage/` is safe
- Your database and files should NOT be affected by Docker cleanup
- The external drive data is separate from Docker's storage

