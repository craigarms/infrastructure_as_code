FROM alpine

RUN apk add ansible --no-cache;\
        mkdir /playbooks /backup

VOLUME /playbooks /backups

ENTRYPOINT ["/usr/bin/ansible-playbook"]
