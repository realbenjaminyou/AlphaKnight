<div align="center">

⚔️ AlphaKnight

The Royal Hall of Classical Chess Engines

Six engines. One bloodline. From a greedy lancer to the Imperator of the board.






Enter the hall, choose your rival, and climb the engine lineage one battle at a time.

</div>

♜ The Chronicle

AlphaKnight is a browser-based chess engine arena built around a family of classical Python chess bots. The project is less about hiding one strong engine behind a polished board and more about preserving the entire climb: each rival represents a different stage in AlphaKnight's development, with new search ideas, evaluation terms, move-ordering techniques, and time-management logic appearing as the ladder rises.

At the bottom stands Lancer, the renamed original AlphaKnight v0: a simple material-driven bot that looks for immediate tactical profit. At the top stands Imperator, the current master engine, with iterative deepening, transposition tables, cached evaluation, pawn-structure hashing, selective pruning, quiescence search, SEE-based tactical filtering, and substantially more sophisticated positional evaluation.

The result is a playable history of the engine itself.

                    THE ROYAL ENGINE LADDER

                         ♛  IMPERATOR
                            ~2000 Elo
                               │
                         ♜  CENTURION
                            ~1900 Elo
                               │
                         ♝  TEMPLAR
                            ~1700 Elo
                               │
                         ♞  PALADIN
                            ~1500 Elo
                               │
                         ♟  TROJAN
                            ~1200 Elo
                               │
                         ♙  LANCER
                             ~800 Elo

Rating note: the Elo numbers are approximate project estimates, not official federation ratings. Actual playing strength changes with hardware, browser performance, time controls, and testing pool.

👑 The Six Houses of AlphaKnight

♛ Imperator — The Crowned Engine

Estimated strength: ~2000 Elo
Role: Current flagship / master rival

Imperator is the strongest AlphaKnight engine in the arena and the most complete expression of the project's classical-search approach. It still follows the same compact interface as the earlier bots, but internally it carries much more machinery.

Search arsenal

Imperator uses iterative deepening, repeatedly completing deeper searches until its soft or hard time boundary is reached. Later iterations use aspiration windows around the previous score instead of beginning every search with the full alpha-beta range. If the position falls outside the window, the engine widens it and searches again.

Its main search combines several standard engine techniques:

Alpha-beta search with principal-variation style re-searches

Transposition-table probing and storage with exact, lower-bound, and upper-bound entries

Null-move pruning in positions where a pass test indicates the side is already comfortably above beta

Late-move reductions (LMR) to spend less depth on moves that appear less promising after strong candidates have already been searched

Late-move pruning for quiet moves in shallow, non-PV positions

Static-evaluation cutoffs / futility-style pruning where a full search is unlikely to change the result

ProbCut-style tactical pruning at deeper non-PV nodes

Check extensions so forcing checking positions receive additional depth

Quiescence search to avoid stopping the search in the middle of unstable capture sequences

Static Exchange Evaluation (SEE) to reject or demote tactically unsound captures

Killer-move and history heuristics for better quiet-move ordering

Staged move ordering that prioritizes transposition-table moves, strong tactical moves, killer moves, and historically successful quiets

Imperator also keeps separate soft and hard time limits, allowing it to stop gracefully after a completed iteration without running dangerously close to the allotted budget.

Evaluation chamber

Imperator's evaluation is tapered between middlegame and endgame values instead of treating every position with one fixed set of weights. Its evaluation includes:

Material values with separate middlegame and endgame weights

Piece-square tables

Game-phase interpolation

Doubled, isolated, supported, passed, candidate, and backward pawn concepts

Pawn phalanxes

Bishop-pair bonuses

Piece mobility

King zones and king-safety pressure

Attacking-piece counts and checking potential

Rook activity on open and semi-open forward files

Pawn threats and pawn-push threats

Endgame scaling for reduced-material positions

Memory of the battlefield

Imperator avoids recalculating everything from nothing. It maintains several caches:

A large transposition table for previously searched positions

A dedicated pawn hash for pawn structures and pawn attack information

An evaluation cache for repeated static evaluations

Incremental base-evaluation state through the search stack

This is one of the largest differences between Imperator and the early AlphaKnight engines: the engine is not simply searching deeper. It is spending its search budget more selectively and reusing work wherever possible.

Character

Imperator is intended to feel disciplined. It can still attack, but it is less likely to throw away long-term structure for a shallow tactical temptation. It is the arena's final exam: the engine where move ordering, pruning, positional evaluation, and tactical verification all meet.

♜ Centurion — The Veteran of the Hall

Estimated strength: ~1900 Elo
Role: Advanced classical rival

Centurion is the bridge between the older tournament engines and Imperator. It already contains many of the ingredients associated with a serious handcrafted chess engine.

Its evaluation includes tapered middlegame/endgame scoring, piece-square tables, pawn structure, pawn phalanxes, king safety, mobility, and broader positional terms. On the search side it uses deep alpha-beta search, SEE, killer/history move ordering, and aspiration search.

Centurion matters in the AlphaKnight lineage because it is where the engine stops feeling primarily tactical and begins behaving like a more rounded positional opponent. It is strong enough to punish loose tactics, but it also has enough evaluation detail to care about structure and king exposure before those weaknesses become immediate combinations.

Centurion's signature tools

Tapered positional evaluation

Piece-square tables

Pawn-structure scoring and pawn phalanxes

King-safety evaluation

Static Exchange Evaluation

Killer and history heuristics

Aspiration-window iterative search

Classical alpha-beta search with quiescence support

If Imperator is the crown, Centurion is the commander that taught the army how to fight as a unit.

♝ Templar — The Tournament Knight

Estimated strength: ~1700 Elo
Earlier designation: AlphaKnight 4

Templar is a standalone classical tournament engine built around stronger search discipline. Its key ideas are less about adding dozens of evaluation terms and more about reducing wasted work.

Core techniques

Transposition tables to reuse searched positions

Late-move reductions to reduce depth on lower-priority moves

Null-move pruning to cut branches that are unlikely to challenge the current bound

King-safety evaluation

Iterative search and tactical extensions typical of the AlphaKnight classical line

Templar is the point in the family where selective search becomes a central weapon. It does not need to examine every branch equally. It tries to identify which branches deserve the most attention.

That makes Templar a useful training opponent for intermediate players: it is much less forgiving of speculative moves than the lower engines, while still remaining more approachable than Centurion or Imperator.

♞ Paladin — The Tactical Guard

Estimated strength: ~1500 Elo
Earlier designation: AlphaKnight 3

Paladin is a tactical alpha-beta engine. Its design is cleaner and more direct than the upper houses, with a strong emphasis on tactical search and basic positional guidance.

Core techniques

Negamax alpha-beta search

Quiescence search at the leaves

Piece-square heuristics

MVV-LVA move ordering (Most Valuable Victim / Least Valuable Attacker)

Tactical capture prioritization

Quiescence search is especially important here. Instead of evaluating a position immediately at the nominal search horizon, Paladin continues through forcing captures so it is less likely to make decisions based on a position that is tactically unfinished.

Paladin is the first opponent in the ladder that should consistently force a player to respect short tactical sequences rather than relying on one-move threats.

♟ Trojan — The Raider

Estimated strength: ~1200 Elo
Earlier designation: AlphaKnight 2

Trojan is the first major step beyond the original baseline. It uses iterative deepening search with positional heuristics and more deliberate tactical evaluation.

The engine remains comparatively lightweight, but it begins to exhibit an important trait that Lancer lacks: it can build a choice from a search tree rather than mostly judging the immediate material outcome of one move.

What Trojan introduces to the bloodline

Iterative deepening

Deeper lookahead than the baseline engine

Positional heuristics

More purposeful tactical move selection

A foundation for the later alpha-beta family

Trojan is intentionally imperfect. That is part of its value. It is a stepping stone between beginner opposition and the stronger search engines above it.

♙ Lancer — The First Banner

Estimated strength: ~800 Elo
Original identity: AlphaKnight v0 / AlphaKnight 1

Lancer is where the story begins.

The original v0 engine was deliberately simple. It evaluates positions mainly by material balance, with standard piece values for pawns, minor pieces, rooks, queens, and kings. Before performing a general evaluation, it checks for an immediate checkmate. If no mate is available, it strongly prefers captures and sorts them by the value of the victim. Otherwise it makes a one-ply material judgment with a small random perturbation.

In simplified form, Lancer's creed is:

1. Can I mate now?
2. Can I take something valuable?
3. Which legal move leaves me with the best material score?

There are no deep transposition tables here. No elaborate pawn hash. No selective pruning tree. No sophisticated king-danger model.

And that is exactly why Lancer belongs in the repository.

It gives AlphaKnight a visible starting point. When compared against Imperator, the difference is not merely a larger Elo number. The full evolution of the project becomes visible: from immediate material greed to structured search, selective pruning, positional scoring, and cached evaluation.

🏰 Engine Lineage at a Glance

Rival

Est. Elo

Search identity

Evaluation identity

Place in the lineage

♙ Lancer

~800

Immediate mate/capture checks, shallow scoring

Material-first

Original baseline, formerly v0

♟ Trojan

~1200

Iterative deepening

Material + positional heuristics

First real search-oriented step

♞ Paladin

~1500

Negamax alpha-beta + quiescence

Piece-square/tactical heuristics

Tactical search engine

♝ Templar

~1700

TT + LMR + null-move pruning

Classical positional + king safety

Selective tournament search

♜ Centurion

~1900

Deep alpha-beta + aspiration + strong ordering

Tapered evaluation, structure, king safety

Advanced all-round engine

♛ Imperator

~2000

Iterative deepening, TT, PVS-style search, null move, LMR, ProbCut, qsearch

Cached tapered evaluation, pawn hash, mobility, threats, king safety

Current flagship

⚙️ One Contract, Six Minds

Despite the differences in strength, the AlphaKnight engines share a deliberately small external interface:

def get_move(fen: str, time_left_ms: int) -> str:
    ...

Each engine receives:

a position in FEN format;

a time budget in milliseconds;

and returns one legal move in UCI notation.

This common contract makes the arena modular. The front end can swap from Lancer to Imperator without learning a new engine API.

Inside the browser, Pyodide runs Python and python-chess. The arena therefore keeps the chess engine logic in Python while the interface, progression systems, board, menus, and game state are driven from the web application.

The current repository is intentionally compact: the arena and embedded engine sources live together in index.html, making GitHub Pages deployment straightforward.

⚔️ The Arena

The engines are the heart of AlphaKnight, but the surrounding arena is designed to make fighting them feel like progression rather than a plain engine test bench.

Difficulty crowns

Mode

Assistance

Reward

Easy

Takebacks + analysis

★

Medium

Takebacks, no analysis

★★

Hard

No takebacks, no analysis

★★★

Each opponent can be challenged at multiple difficulty levels, turning the engine ladder into a star-based progression system.

Training systems

Opening Practice — lock the beginning of a game into a selected opening line and practice the resulting positions.

Odds Chess — begin with a material edge and practice converting it against an engine.

What If Sandbox — return to an earlier position, test a variation, then restore the official game.

Achievements — complete challenges such as winning without castling or defeating Imperator quickly.

Style Archetypes — build a profile based on tendencies shown across games.

Optional clocks — play untimed or with a royal match timer.

The interface uses a medieval chess-club theme so the engine ladder feels like entering successive halls of the same kingdom rather than choosing values from a debug dropdown.

🛡️ Why Build Several Engines?

A single strongest engine would be simpler. It would also erase most of the interesting history.

AlphaKnight keeps its older engines because they make the improvement process playable. The differences between generations reveal what individual techniques actually change:

Lancer shows the limits of material-only reasoning.

Trojan shows what happens when real lookahead enters the picture.

Paladin shows the effect of alpha-beta search, move ordering, and quiescence.

Templar shows the value of selective pruning and transposition reuse.

Centurion shows the benefit of a broader positional evaluation.

Imperator combines these ideas with more aggressive search control, caching, and pruning.

The ladder is therefore both a game mode and a record of engine development.

🧪 Running the Royal Hall Locally

Clone the repository:

git clone https://github.com/realbenjaminyou/AlphaKnight.git
cd AlphaKnight

Serve the project with a small local HTTP server:

python -m http.server 8000

Then open:

http://localhost:8000

The browser loads Pyodide and installs/loads the Python chess runtime used by the embedded agents, so an internet connection may be needed on first load depending on browser caching.

🗺️ Repository Layout

AlphaKnight/
├── index.html      # Arena UI, browser bridge, progression systems, and embedded engines
└── README.md       # The chronicle you are reading

The minimal layout is intentional. The project can be deployed directly through GitHub Pages without a separate backend engine service.

🔨 For Engine Tinkerers

If you want to add another AlphaKnight rival, the simplest path is to preserve the same engine contract:

def get_move(fen: str, time_left_ms: int) -> str:
    # Build/search the position.
    # Return a legal UCI move such as "e2e4".
    return best_move

A new generation can then be compared against the existing ladder under the same arena conditions.

Useful areas to experiment with include:

move-ordering heuristics;

pruning thresholds;

evaluation weights;

pawn-structure scoring;

time allocation;

transposition-table replacement policy;

endgame scaling;

search extensions and reductions.

For meaningful comparisons, test engines over many games with fixed time controls and alternating colors. A handful of showcase wins is not enough to establish Elo.

📜 Naming the Order

The medieval names are not separate unrelated bots. They are a lineage.

Generation

Arena name

Identity

I

Lancer

Original AlphaKnight v0 baseline

II

Trojan

Early iterative-search engine

III

Paladin

Tactical alpha-beta engine

IV

Templar

Selective tournament engine

V

Centurion

Advanced positional/search engine

VI

Imperator

Current flagship

The names make the progression legible in the arena while preserving the development story underneath.

<div align="center">

♛ The throne is only sixty-four squares wide.

Choose a rival. Learn its habits. Climb the hall.

Repository · Issues · Pull Requests

Made by Benjamin You.

</div>
