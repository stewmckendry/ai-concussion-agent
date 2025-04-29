## 🛠 E2E Flow: Way of Working

╔═════════════════════════════════════╗
║          1. DeliveryPod Plans        ║
╠═════════════════════════════════════╣
║ /tasks/activate                      ║
║ - Marks task as "planned"            ║
║ - Links planned prompt if available  ║
║ - (No actual start yet)              ║
╚═════════════════════════════════════╝
             ↓

╔═════════════════════════════════════╗
║         2. Execution Pod Begins      ║
╠═════════════════════════════════════╣
║ /tasks/start                         ║
║ - Pod pulls next planned task        ║
║ - Auto-fetches prompt (or drafts)    ║
║ - Captures prompt_used.txt           ║
║ - Initializes reasoning trace        ║
║ - Auto-commits                        ║
╚═════════════════════════════════════╝
             ↓

╔═════════════════════════════════════╗
║        3. Pod Works on Task          ║
╠═════════════════════════════════════╣
║ Normal work cycle: deliverables,     ║
║ chain_of_thought updates, interim    ║
║ auto-commits                         ║
╚═════════════════════════════════════╝
             ↓

╔═════════════════════════════════════╗
║      4. Pod Finishes Task            ║
╠═════════════════════════════════════╣
║ /tasks/complete                      ║
║ - Marks task "done"                  ║
║ - Final reasoning_trace.md update    ║
║ - Update task.yaml, memory.yaml      ║
║ - Auto-commit completion             ║
╚═════════════════════════════════════╝
             ↓

╔═════════════════════════════════════╗
║        5. System Suggests Next       ║
╠═════════════════════════════════════╣
║ If next task is clear:               ║
║ - Auto-activate next task            ║
║ Else:                                ║
║ - Wait for DeliveryPod direction     ║
╚═════════════════════════════════════╝
             ↓

╔═════════════════════════════════════╗
║       6. Handling Handoffs           ║
╠═════════════════════════════════════╣
║ On Pod transition, system checks:    ║
║ - Handoff notes                      ║
║ - Chain of Thought                   ║
║ - Open tasks                         ║
╚═════════════════════════════════════╝

