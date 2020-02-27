# Environment Variables Lab

## Timings

45 - 60 Minutes

## Summary

We know how to set environment variables and how to persist them between logins by adding them to the bashrc file. 

But we're using Vagrant to automatically create environments and we don't want the developers to have to do this manually.

We need to use an environment variable to tell the app the location of the database running on the db VM. 

```
mongodb://192.168.10.150:27017/posts
```

## Tasks

* Write a bash command that will inject an export line in to the bashrc
* Use Vagrant a shell provisioner to run this command
* Use your script to create an environment variable called DB_HOST with the correct value for connecting to the database
* Start the app and ensure that the /posts route is now connected correctly

## Bonus

Use ruby to create a method that allows you to easily add more environment variables in the future as needed.

## Tips

the HEREDOC syntax in ruby is a useful way to create big blocks of code as strings.
