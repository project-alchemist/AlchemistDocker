# Alchemist Docker Image

In order to run use the following commands:

```bash
docker build -t alchemist:0.2 .
docker run -p 24960-24970:24960-24970 --name alchemist alchemist:0.2
```

or via `docker-compose`:

```bash
docker-compose up
```

Make sure to create `.env` file with proper git hashes (look at `.default.env` example).
