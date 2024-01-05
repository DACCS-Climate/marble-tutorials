# Troubleshooting

## FAQ

**My saved files are missing**

Only files saved in the `writable-workspace` folder will be kept when the user exits JupyterLab or the server shuts down.

Files saved in all other locations are not kept.


**My git repository is missing**

If the git repository was created in a public folder, such as `mypublic`, it is possible the files were cleaned out when the server shut down. Only files saved in the `writable-workspace` folder will be kept.

If the git repository interface is not displaying when expected, perhaps you have not navigated into the folder where the git repository resides.