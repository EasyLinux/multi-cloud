FROM alpine:3.12 AS Build
LABEL author="Serge NOEL <serge.noel@easylinux.fr>"

RUN apk add go git build-base pkgconf libvirt-dev

RUN mkdir /app
WORKDIR /app
RUN git clone https://github.com/dmacvicar/terraform-provider-libvirt.git .
RUN go build 


FROM alpine:3.12
LABEL author="Serge NOEL <serge.noel@easylinux.fr>"

RUN mkdir -p /root/.terraform.d/plugins/linux_amd64/
COPY --from=Build /app/terraform-provider-libvirt /root/.terraform.d/plugins/linux_amd64/
# terraform-provider-libvirt

RUN apk add --no-cache terraform libvirt gcc libxslt cdrkit openssh-client \
    && mkdir /app

WORKDIR /app
VOLUME /app
