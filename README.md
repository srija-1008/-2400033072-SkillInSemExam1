# -2400033072-SkillInSemExam1
The Event Calendar component displays a simple calendar for the current month. Users can click a date to see any events scheduled for that day.
import React, { useState } from "react";

const EventCalendar = () => {
  const [selectedDate, setSelectedDate] = useState(null);

  const events = [
    { date: "2025-10-10", title: "Project Deadline", description: "Submit report" },
    { date: "2025-10-14", title: "Team Meeting", description: "Sprint planning" },
    { date: "2025-10-20", title: "Workshop", description: "React basics" },
  ];

  const today = new Date();
  const year = today.getFullYear();
  const month = today.getMonth();
  const firstDay = new Date(year, month, 1).getDay();
  const days = new Date(year, month + 1, 0).getDate();

  const formatDate = d => `${year}-${String(month + 1).padStart(2, "0")}-${String(d).padStart(2, "0")}`;
  const selectedEvents = events.filter(e => e.date === selectedDate);

  return (
    <div style={{ textAlign: "center", fontFamily: "sans-serif" }}>
      <h2>{today.toLocaleString("default", { month: "long" })} {year}</h2>
      <div style={{ display: "grid", gridTemplateColumns: "repeat(7, 1fr)", gap: 6 }}>
        {[...Array(firstDay).keys()].map(i => <div key={i}></div>)}
        {[...Array(days).keys()].map(i => {
          const date = formatDate(i + 1);
          const isSel = selectedDate === date;
          const hasEvent = events.some(e => e.date === date);
          return (
            <div
              key={i}
              onClick={() => setSelectedDate(date)}
              style={{
                padding: 10,
                borderRadius: 6,
                cursor: "pointer",
                background: isSel ? "#4CAF50" : hasEvent ? "#dfffd6" : "#f4f4f4",
                color: isSel ? "#fff" : "#000",
              }}
            >
              {i + 1}
            </div>
          );
        })}
      </div>

      <div style={{ marginTop: 20 }}>
        {selectedDate ? (
          selectedEvents.length ? (
            selectedEvents.map((e, i) => <p key={i}><b>{e.title}</b>: {e.description}</p>)
          ) : <p>No events</p>
        ) : <p>Select a date</p>}
      </div>
    </div>
  );
};

export default EventCalendar;


