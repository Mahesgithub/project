# Medical Appointment Scheduling Agent — Simple Root Map (Short & Clear)

## Project root (concise tree)

```
appointment-scheduling-agent/
├── README.md
├── .env.example
├── requirements.txt
├── architecture_diagram.png
├── backend/
│   ├── main.py
│   ├── agent/
│   │   ├── scheduling_agent.py
│   │   └── prompts.py
│   ├── rag/
│   │   ├── faq_rag.py
│   │   ├── embeddings.py
│   │   └── vector_store.py
│   ├── api/
│   │   ├── chat.py
│   │   └── calendly_integration.py
│   ├── tools/
│   │   ├── availability_tool.py
│   │   └── booking_tool.py
│   └── models/
│       └── schemas.py
├── frontend/ (optional)
│   └── src/
│       ├── App.jsx
│       └── components/
│           ├── ChatInterface.jsx
│           └── AppointmentConfirmation.jsx
├── data/
│   ├── clinic_info.json
│   └── doctor_schedule.json
└── tests/
    └── test_agent.py
```

## One-line purpose for key files/folders

* `backend/main.py` — FastAPI app entry, mounts routes and middleware.
* `backend/agent/scheduling_agent.py` — Conversation manager; handles dialog state, slot-filling, context switching (scheduling ↔ FAQ).
* `backend/agent/prompts.py` — Centralized LLM prompts and templates (booking flow, clarification, confirmation).
* `backend/rag/faq_rag.py` — RAG orchestration: retrieve relevant FAQ docs, build context for LLM answers.
* `backend/rag/embeddings.py` — Embed FAQ documents and user queries (wrapper for chosen embedding model).
* `backend/rag/vector_store.py` — Vector DB interface (Chroma/Pinecone/Qdrant abstraction).
* `backend/api/chat.py` — Chat REST endpoints (receive messages, return agent replies, expose conversation id).
* `backend/api/calendly_integration.py` — Real or mock Calendly endpoints wrapper (availability, booking, cancel, reschedule).
* `backend/tools/availability_tool.py` — Business logic to compute free slots, apply buffers, duration matching.
* `backend/tools/booking_tool.py` — Booking flow: validate inputs, call Calendly, save metadata.
* `backend/models/schemas.py` — Pydantic schemas for requests/responses (BookingRequest, AvailabilityResponse, ChatMessage).
* `frontend/` — React chat UI (optional), shows chat, slot picker, confirmation modal.
* `data/clinic_info.json` — FAQ and clinic metadata used by RAG.
* `data/doctor_schedule.json` — Seed schedule used by mock Calendly.
* `tests/test_agent.py` — Example unit/integration tests (booking, FAQ retrieval, edge cases).

## Minimal conversation flow (compact)

1. User: I want to book → Agent: Ask reason → determine appointment type & duration.
2. Agent: Ask date/time preference → call availability_tool → show 3 suggested slots.
3. User selects slot → Agent: Collect patient name, phone, email → confirm details.
4. Agent: Call booking_tool → create appointment (Calendly) → return confirmation.

(If user asks FAQ mid-flow: run RAG, answer, then restore booking state.)

## Smart scheduling rules (short)

* Match slot length to appointment type (30/15/45/60 min).
* Apply buffer (e.g., 10 minutes) between appointments.
* Avoid double-booking by checking existing events.
* If no slots: offer nearest dates, waitlist instruction, or phone contact.

## Quick API endpoints (suggested)

* `POST /api/chat` — Send user message, returns agent reply + suggested actions.
* `GET /api/calendly/availability?appointment_type=&date=` — List slots for date.
* `POST /api/calendly/book` — Book appointment (body: appointment_type, date, start_time, patient, reason).
* `POST /api/calendly/cancel` — Cancel booking by id.
* `POST /api/calendly/reschedule` — Reschedule booking.

## README highlights (what to write briefly)

* Setup (env, pip install), how to run FastAPI, how to configure LLM & vector DB.
* How to switch between real Calendly and mock mode.
* Short system diagram and sample conversations.

## Testing & edge cases to include (short list)

* Booking happy path; missing fields; ambiguous times; no availability; API timeout/failure.
* RAG correctness: return source snippet + citation.

---

If you want, I can also generate a one-page architecture diagram (ASCII or PNG-ready description) or a very short `main.py` skeleton next. Which would you like next?
