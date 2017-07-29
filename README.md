Forked from [Robert Beene](https://github.com/rbeene/phoenix-with-docker)
##### Build

```shell
docker-compose up -d
docker-compose run web mix phoenix.new hello_world
mv hello_world/* ./
mv hello_world/.gitignore ./
rm -rf hello_world
# don't forget to rename your database hostname, you remember this step - right?
docker-compose run web mix ecto.create
docker-compose restart web
```

> Did you get an error when creating the database? I purposefully left out a step. Remember the hostname needs to match the names of your containers. If you look inside the new phoenix application, you'll find a file `config\dev.exs`. At the bottom of this file, it gives `localhost` for the hostname of the database server. In the land of docker, we're calling it `db`. Make that change and try to create the database again.

If all goes well, go to localhost:4000.

With this setup, you can get up and running on any machine running docker and know your environment is exactly the same. In development, qa, and production - you can keep everything in lock step. For production, you'll want to consult with your devops team to ensure the configuration is in line with what they want. Consider this a starting point.