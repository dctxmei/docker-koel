# docker-koel

This project depends on [Hyzual/docker-koel][Hyzual/docker-koel] .

Rewrite the docker-compose.yml file to better run the [Koel][Koel] project.

---

Do you need a private streaming music site? Koel can meet your requirements,
but [deploying][Manually] it will easily pollute the operating environment, so
I choose to use [Docker][Docker].

After deployment, you can easily combine it with other services (Nginx), or use
[WireGurad][WireGurad] at the same time to get more secure and efficient data
transmission.

In Docker, the path for Koel to store music is `/music`, and on the host
machine, because the storage volume is used, the path is
`/var/lib/docker/volumes/<volume_name_for_koel>/_data` .

Come and enjoy the music!

## Usage

0. The Docker Engine version needs to be greater than 18.02.0, and the Compose
   file format 3.6 version is used here.
1. You need to manually modify the `root_password` and `koel_password` in the
   docker-compose.yml file.
2. Clone the repository:

    ```
    $ git clone https://github.com/dctxmei/docker-koel.git
    ```

3. Execute docker-compose.yml:

    ```
    $ cd docker-koel/
    $ docker-compose up -d
    ```

4. Initial content (If the content already exists, this step is not necessary):

    ```
    $ docker exec -it <container_name_for_koel> bash
    $ php artisan koel:init
    ```

## Ports

### 80

To run Koel, it is not recommended to use HTTP for transmission directly, but
to deploy HTTPS through a reverse proxy.

### 8080

To run [Adminer][Adminer], my suggestion is the same as that of Koel mentioned above.

[Hyzual/docker-koel]: https://github.com/Hyzual/docker-koel
[Koel]: https://koel.dev/
[Manually]: https://docs.koel.dev/#manually
[Docker]: https://www.docker.com/
[WireGurad]: https://www.wireguard.com/
[Adminer]: https://www.adminer.org/

## Remove

```
$ cd docker-koel/
$ docker-compose down
```

You may also need to manage storage volumes through `docker volume`.
