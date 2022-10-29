FROM mcr.microsoft.com/dotnet/sdk:6.0 as debug

#install debugger for NET Core
RUN apt-get update
RUN apt-get install -y unzip
RUN curl -sSL https://aka.ms/getvsdbgsh | /bin/sh /dev/stdin -v latest -l ~/vsdbg

RUN mkdir /work/
WORKDIR /work/
EXPOSE 7030
EXPOSE 5165

COPY ./dotnet-docker.csproj /work/dotnet-docker.csproj
RUN dotnet restore

COPY . /work/
RUN mkdir /out/
RUN dotnet publish --no-restore --output /out/ --configuration Release

RUN dotnet dev-certs https --clean
RUN dotnet dev-certs https -t

CMD dotnet watch run