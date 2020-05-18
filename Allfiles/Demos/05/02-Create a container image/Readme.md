# Create a Dockerfile for a the web app

1. In a command prompt on your local computer, create a folder for the project and then run the
following command to download the source code for the web app.
``` html
git clone https://github.com/MicrosoftDocs/mslearn-hotel-reservation-system.git
```

2. Move to the src folder

``` cmd
cd mslearn-hotel-reservation-system/src
```

3. In this directory, create a new file named Dockerfile with no file extension and open it in a text editor.

``` cmd
echo "" > Dockerfile
notepad Dockerfile
```

4. Add the following commands to the Dockerfile.
``` dockerfile
#1
FROM mcr.microsoft.com/dotnet/core/sdk:2.2
WORKDIR /src
COPY ["HotelReservationSystem/HotelReservationSystem.csproj", "HotelReservationSystem/"]
COPY ["HotelReservationSystemTypes/HotelReservationSystemTypes.csproj", "HotelReservationSystemTypes/"]
RUN dotnet restore "HotelReservationSystem/HotelReservationSystem.csproj"
#2
COPY . .
WORKDIR "/src/HotelReservationSystem"
RUN dotnet build "HotelReservationSystem.csproj" -c Release -o /app
#3
RUN dotnet publish "HotelReservationSystem.csproj" -c Release -o /app
#4
EXPOSE 80
WORKDIR /app
ENTRYPOINT ["dotnet", "HotelReservationSystem.dll"]
```

5. Save the file and close your text editor
