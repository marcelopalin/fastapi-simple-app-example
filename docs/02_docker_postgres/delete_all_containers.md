https://www.digitalocean.com/community/tutorials/how-to-remove-docker-images-containers-and-volumes-pt

Parar e remover todos os contêineres
Você pode revisar os contêineres em seu sistema com o docker ps. Adicionando a flag -a mostrará todos os contêineres. Quando você tiver certeza de que deseja excluí-los, você pode adicionar a flag -q para fornecer os IDs para os comandos docker stop e docker rm:

Listar:

docker ps -a
 
Remover:

docker stop $(docker ps -a -q)
docker rm $(docker ps -a -q)
