FROM alpine:3 As downloader
ARG DOWNLOAD_LOCATION="https://github.com/nopSolutions/nopCommerce/releases/download/release-4.60.6/nopCommerce_4.60.6_NoSource_linux_x64.zip"
ADD ${DOWNLOAD_LOCATION} /nopCommerce/nopCommerce_4.60.6_NoSource_linux_x64.zip
RUN apk update && \
    apk add unzip && \
    cd /nopCommerce && \
    unzip nopCommerce_4.60.6_NoSource_linux_x64.zip && mkdir bin logs \
    && rm nopCommerce_4.60.6_NoSource_linux_x64.zip
    
FROM mcr.microsoft.com/dotnet/sdk:7.0
LABEL game="play"
COPY --from=downloader nopCommerce /nopCommerce
ENV ASPNETCORE_URLS="http://0.0.0.0:5000"
EXPOSE 5000
WORKDIR /nopCommerce
CMD [ "dotnet", "Nop.Web.dll" ]