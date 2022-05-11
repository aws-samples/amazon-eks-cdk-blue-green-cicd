FROM public.ecr.aws/p8v8e7e5/myartifacts:alpine-jan2021


ENV KUBECONFIG /home/kubectl/.kube/kubeconfig
ENV HOME /home/kubectl
# ENV KUBECONFIG /root/.kube/kubeconfig


RUN \
	mkdir /root/bin /aws; \
	apk -Uuv add groff less bash python3 py-pip jq curl docker && \
	pip3 install --upgrade pip; \
	pip3 install awscli && \
	rm /var/cache/apk/* && \
	# Create non-root user (with a randomly chosen UID/GUI).
	adduser kubectl -Du 5566

ADD https://s3.us-west-2.amazonaws.com/amazon-eks/1.22.6/2022-03-09/bin/linux/amd64/kubectl /usr/local/bin/kubectl
#COPY kubectl /usr/local/bin/kubectl

WORKDIR $HOME

COPY entrypoint.sh /usr/local/bin/entrypoint.sh

RUN chmod a+x /usr/local/bin/kubectl /usr/local/bin/entrypoint.sh

VOLUME /var/lib/docker

# USER kubectl
ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]
