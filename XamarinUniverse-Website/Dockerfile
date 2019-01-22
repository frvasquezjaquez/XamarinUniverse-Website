#Depending on the operating system of the host machines(s) that will build or run the containers, the image specified in the FROM statement may need to be changed.
#For more information, please see https://aka.ms/containercompat

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src

#Copy csproj and restore as distinct layers
COPY *.csproj ./
RUN dotnet restore

COPY . .
RUN dotnet build -c Release -o /app

FROM build AS publish
RUN dotnet publish -c Release -o /app

FROM microsoft/dotnet:2.1-aspnetcore-runtime AS final
WORKDIR /app
EXPOSE 80
EXPOSE 443
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "XamarinUniverse-Website.dll"]