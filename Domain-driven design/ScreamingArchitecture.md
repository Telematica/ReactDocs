# Screaming Architecture

- https://blog.cleancoder.com/uncle-bob/2011/09/30/Screaming-Architecture.html
- https://www.linkedin.com/feed/update/urn:li:activity:7243514747634040832/
- https://dev.to/profydev/screaming-architecture-evolution-of-a-react-folder-structure-4g25
- https://medium.com/@mubashirhussain29/the-screaming-architecture-story-08750691291f
- https://levelup.gitconnected.com/what-is-screaming-architecture-f7c327af9bb2
- https://withoutdebugger.com/2023/11/25/screaming-architecture/

If you look at your application and you only see folders like these:

❌
📁 App
|__ 📁API
|__ 📁Models
|__ 📁Views
|__ 📁Controllers
|__ 📁DTOs
|__ 📁Database
|__ ...

Then your app doesn't tell anything about the problem it solves.

It's driven by technology instead of the domain.

If you want to add a new feature, you need to add files to all these places. 

Features are mixed, leading to maintenance hell.

Now look at this folder structure:

✅
📁 CarRentalService
|__ 📁AutoPicker
|__ 📁UserManager
|__ 📁PaymentGateway
|__ 📁InvoiceGenerator
|__ 📁SupportCenter
|__ ...

It is called screaming architecture. It screams the domain.

It is easy to navigate, with clear domain separations.

If you want to add a new feature, you just add a new main directory.

It has better discoverability and results in a low entry curve for new developers.

A clean folder structure is like a well-organized room; everything has its place, and it's easy to find what you need.

Your folder structure should communicate the domain, not the technology.