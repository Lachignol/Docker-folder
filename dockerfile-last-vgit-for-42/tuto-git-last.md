CREATE DIRECTORY WITH DOCKERFILE IN THIS FOLDER

1-
Construisez l’image avec docker build -t git-nonroot-builder .

2-
Lancez un container en arrière-plan avec docker run -d --name git-builder git-nonroot-builder tail -f /dev/null
Supprimez le container si besoin avec docker rm -f git-builder

3-
Copier les fichiers depuis Docker vers local

bash
```
docker cp git-builder:/home/usergit/.local/bin/git ~/.local/bin/
docker cp git-builder:/home/usergit/.local/libexec ~/.local/
docker cp git-builder:/home/usergit/.local/share ~/.local/
```

4-
maj les path pour que notre binaire git soit apeler en premier et lui donner les chemin des ses utils
bash
```
export PATH="$HOME/.local/bin:$PATH"
export GIT_EXEC_PATH="$HOME/.local/libexec/git-core"
```

