# Online_Booking_System

An online bus booking system built with ASP.NET Web Forms (C#, .NET Framework 4.5) and SQL Server. This repository contains the admin module of the application (`BusBookingProject`) and the SQL Server script for the `OnlineBusBooking` database.

## Features

The admin pages (under `Admin/`) let an administrator:

- Log in to the admin area (pages redirect to the login page when there is no admin session)
- Add new buses and update existing ones (bus number, name, type, seat rows and columns, origin and destination)
- View a bus details report, with links to edit a bus or add a schedule for it
- Add bus schedules (date, fare, travel time, arrival and departure times)
- View route details and add boarding (pick-up) points with their times for a route
- View a booking report of all tickets booked by users

The database script also defines tables and stored procedures for the customer side of the system (user registration and login, searching available buses, seat selection, passenger details, card payment details and PNR generation). The customer-facing pages themselves are not included in this repository.

## Tech Stack

- ASP.NET Web Forms, C#, .NET Framework 4.5
- Microsoft SQL Server (ADO.NET with stored procedures)
- Bootstrap, jQuery, Font Awesome
- iTextSharp (DLLs included in `bin/`)

## Project Structure

```
Online_Booking_System/
├── Admin/                     Admin module (Web Forms pages and code-behind)
│   ├── Admin.Master           Master page with the admin navigation bar
│   ├── AdminLogin.aspx        Admin login
│   ├── Default.aspx           Admin home page
│   ├── BusDetails.aspx        Add / update a bus
│   ├── BusDetailsReport.aspx  List of buses with edit and schedule links
│   ├── BusScheduleDetails.aspx Add a schedule for a bus
│   ├── RouteDetails.aspx      List of routes
│   ├── BoardingDetails.aspx   Add boarding points for a route
│   ├── BookingReport.aspx     Report of all bookings
│   ├── css/, fonts/, js/      Admin static assets
├── bin/                       Compiled BusBookingProject.dll, its config, and iTextSharp DLLs
├── css/, fonts/, js/          Site-wide static assets (Bootstrap, jQuery, Font Awesome)
├── database/
│   └── OnlineBusBooking.sql   Script that creates the database, tables and stored procedures
└── Properties/                Assembly info and publish profile
```

Note: the repository does not include a Visual Studio project/solution file (`.csproj`/`.sln`), a root `Web.config`, or the public (non-admin) pages.

## Prerequisites

- Windows
- Visual Studio with ASP.NET and web development support (.NET Framework 4.5 targeting pack), or IIS
- Microsoft SQL Server (e.g. SQL Server Express) and SQL Server Management Studio

## Setup

1. Clone the repository:

   ```
   git clone https://github.com/iSouvikKhan/Online_Booking_System.git
   ```

2. Create the database: open `database/OnlineBusBooking.sql` in SQL Server Management Studio and execute it. It creates the `OnlineBusBooking` database with its tables and stored procedures.

3. Configure the connection string. The code reads a connection string named `OnlineBusBookingConnectionString`:

   ```xml
   <connectionStrings>
     <add name="OnlineBusBookingConnectionString"
          connectionString="Data Source=YOUR_SERVER;Initial Catalog=OnlineBusBooking;Integrated Security=True"
          providerName="System.Data.SqlClient"/>
   </connectionStrings>
   ```

   The included `bin/BusBookingProject.dll.config` points to the original developer's machine, so change `Data Source` to your own SQL Server instance.

4. Open the project in Visual Studio. Because no project file is included, create an empty ASP.NET Web Application (.NET Framework 4.5) named `BusBookingProject`, add the repository files to it, add references to the iTextSharp DLLs in `bin/`, and put the connection string above in the project's `Web.config`.

## Running

Run the web application from Visual Studio (F5) and open `Admin/AdminLogin.aspx` in the browser. After logging in you are taken to the Bus Details Report page, and the navigation bar gives access to the other admin pages.

The admin credentials are hard-coded in `Admin/AdminLogin.aspx.cs`; change them before using the application anywhere other than a local machine.
