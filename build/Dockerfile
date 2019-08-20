FROM nginx:1.17.3

# forward nginx access and error logs to stdout and stderr of the ingress
# controller process
RUN mkdir -p /etc/nginx/run/log/nginx \
	&& ln -sf /proc/1/fd/1 /etc/nginx/run/log/nginx/access.log \
	&& ln -sf /proc/1/fd/1 /etc/nginx/run/log/nginx/stream-access.log \
	&& ln -sf /proc/1/fd/2 /etc/nginx/run/log/nginx/error.log \
	&& apt-get update \
	&& apt-get install -y libcap2-bin \
	&& setcap 'cap_net_bind_service=ep' /usr/sbin/nginx 

COPY nginx-ingress internal/configs/version1/nginx.ingress.tmpl internal/configs/version1/nginx.tmpl internal/configs/version2/nginx.virtualserver.tmpl /

RUN rm /etc/nginx/conf.d/*

RUN mkdir -p /etc/nginx/secrets

# Uncomment the line below if you would like to add the default.pem to the image
# and use it as a certificate and key for the default server
# ADD default.pem /etc/nginx/secrets/default

ENTRYPOINT ["/nginx-ingress"]
