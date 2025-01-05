### Uninstalling longhorn

```bash
# change to true
kubectl -n longhorn-system edit settings.longhorn.io deleting-confirmation-flag
helm uninstall -n longhorn-system longhorn
```
