all: docker-build
.PHONY: activate docker-build docker-push

# ===================== Docker args
IMAGE_NAME = compiler-s20-env

# Do not named user and group the same, this would cause error in entrypoint.sh
#	because we create the group before user exist which allowing name-crash in useradd command
CONTAINER_USERNAME = student
CONTAINER_GROUPNAME = studentg

HOST_NAME = compiler-s20
HOMEDIR = /home/$(CONTAINER_USERNAME)

DOCKERHUB_ACCOUNT=ianre657

# ===================== end Docker args

docker-push: docker-build
	docker login && docker tag ${IMAGE_NAME} ${DOCKERHUB_ACCOUNT}/${IMAGE_NAME}:latest && docker push

docker-build:
	${MAKE} \
		IMAGE_NAME=${IMAGE_NAME} \
		CONTAINER_USERNAME=${CONTAINER_USERNAME}\
		CONTAINER_GROUPNAME=${CONTAINER_GROUPNAME}\
		CONTAINER_HOMEDIR=${HOMEDIR}\
		HOMEDIR=${HOMEDIR} \
		-C docker


# TODO: change --imagename to our official repo:image
# we call activate_docker.py to share our args between scripts 
activate:
	python3 docker/activate_docker.py \
		--username ${CONTAINER_USERNAME} \
		--homedir ${HOMEDIR} \
		--imagename ${IMAGE_NAME} \
		--hostname ${HOST_NAME}