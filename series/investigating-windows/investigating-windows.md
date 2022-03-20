# Investigating Windows

### **Whats the version and year of the windows machine?**

```
winver
```

### **Which user logged in last?**

```
eventvwr
```

### **When did John log onto the system last?**

```
net user john | findstr "Last logon"
```

