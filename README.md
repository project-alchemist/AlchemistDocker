# Alchemist Docker Image

In order to run use the following commands (you need to have `docker-compose` installed):

```bash
docker-compose up --build alchemist
```

It will build 2 images (base image and alchemist image) and start alchemist.

Make sure to create `.env` file with proper git hashes (look at `.default.env` example).
