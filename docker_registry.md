# Docker Registry
�i�H�ΨӦs��docker image���a��A���������M�p���C����������[Dockerhub](https://hub.docker.com), [Quay](https://quay.io)���O�i�H�s��M���ɪ��a��A�O�i�H���}�s�����A������M���ɩԤU�ӧY�i�ϥΡA�p���������A�ثe�T�j���A�ȳ������ѩ�m�M���ɪ��a��A**AZURE-__azure container registry__**, **AWS-__amazon elastic container registry__**, **GCP-__container registry__**�C�t�~�]�i�H�b���a�ݬ[�]�p�����s��w�C

## Pratice:

���B�p����docker registry ���إH�α��e�M����(�Hubuntu����)

### ���a��(�p��)

�w��docker

```cmd
sudo apt-get update
sudo apt-get install docker.io
```

�b�w�˦ndocker����A�H�e�����Φ��ӫإ�docker registry

```cmd
docker run -d -p 5000:5000 --restart=always --name registry \
-v $(pwd)/data:/var/lib/registry \
registry:2
```

> -v �� host �P container �n�i��P�B���ؿ��A�D�n�s�� docker images ���

�t�~���F��K�˵��A�i�H�A���ݤ@�Ӯe�� docker registry UI ���˵��M����

```cmd
docker run -d -p 5001:80 \
-e ENV_DOCKER_REGISTRY_HOST={HOST IP} \
-e ENV_DOCKER_REGISTRY_PORT=5000 \
konradkleine/docker-registry-frontend:v2
```

�Q���s�����i�JUI���[��

> http://localhost:5001

�N�M���ɱ��W���a�ݪ�registry
(�p�G�S���i�H���Ԥ@�Ӥ��}���M���ɤU��)

```cmd
docker pull mysql
```

�аO�ۤv���M����
```cmd
docker tag mysql localhost:5000/mysql
```

�Nlocalhost:5000/mysql���W���a�ݪ�registry

```cmd
docker push localhost:5000/mysql
```

�A�hUI�W�T�{�A�N�|�h�@��repository

*�L�k�R����@�M���ɡA�u��N���repository�R���άO�R������*

### ����(���� dockerhub)

�n�J container registry

```cmd
az acr login --name mygistry
```

�άO

```cmd
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
  ```
  
�b�N�M�����e�ܱz���n�����e�A�����ϥ� ACR �n�J���A���W�٨ӼаO�M���C �ϥ� docker tag �R�O�ӼаO�M���C �N�n�J���A�����N���z���e�O�����n�J���A���W�١C

```cmd
docker tag <image repository name> <login server>/<image name>:<version>
```

��§�image ���Wdockerhub

```cmd
docker push <username>/<repo name>:<Tag name>
```

�̫��image���e�Wcontainer registry

```cmd
docker push <login server>/<repo name>:<Tag name>
```
