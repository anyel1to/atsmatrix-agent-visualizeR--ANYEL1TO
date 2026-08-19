import requests

ATSMATRIX_ENDPOINT = "http://localhost:8080/api/agent/event"

def emit_step(agent_id: str, action: str, message: str, cluster: str = "VERIFY"):
    requests.post(ATSMATRIX_ENDPOINT, json={
        "agent_id": agent_id,
        "action": action,       # LINK, VERIFY, MATCH, FLAG, SYNC, FOUND
        "cluster": cluster,     # COLLECT, MATCH, CROSS-LINK, VERIFY, SYNTH
        "message": message
    })

# Example inside a LangGraph / CrewAI node:
emit_step("agent_501", "VERIFY", "Cross-verified citation tree with cluster #2", cluster="VERIFY")
emit_step("agent_501", "LINK", "Supplier dependency bridge created", cluster="CROSS-LINK")