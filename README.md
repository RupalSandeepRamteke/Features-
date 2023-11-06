



1. Create a new ASP.NET Core project using your preferred de
public class Schedule
{
    public int Id { get; set; }
    public string Title { get; set; }
    public DateTime StartTime { get; set; }
    public DateTime EndTime { get; set; }
}
```

3. Create a controller to handle the scheduling:

```csharp
using Microsoft.AspNetCore.Mvc;
using System;
using System.Collections.Generic;

[ApiController]
[Route("api/schedules")]
public class ScheduleController : ControllerBase
{
    private List<Schedule> schedules = new List<Schedule>();

    [HttpGet]
    public ActionResult<IEnumerable<Schedule>> GetSchedules()
    {
        return Ok(schedules);
    }

    [HttpPost]
    public ActionResult<Schedule> CreateSchedule([FromBody] Schedule newSchedule)
    {
        // In a real application, you'd likely save the new schedule to a database.
        // For simplicity, we'll just add it to the list here.
        schedules.Add(newSchedule);
        return CreatedAtAction(nameof(GetSchedules), new { id = newSchedule.Id }, newSchedule);
    }
}
```

4. Configure your API in `Startup.cs`:

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddControllers();
}

public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
{
    if (env.IsDevelopment())
    {
        app.UseDeveloperExceptionPage();
    }
    else
    {
        app.UseHsts();
    }

    app.UseHttpsRedirection();
    app.UseRouting();
    app.UseEndpoints(endpoints =>
    {
        endpoints.MapControllers();
    });
}
```
