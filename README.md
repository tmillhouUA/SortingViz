# Simple Sorting Algorithms

An animated, single-file visualizer of three simple sorting algorithms (bubble, selection, and insertion sort), designed for presenting to non-technical audiences on a big screen.

**Live page:** https://tmillhouua.github.io/SortingViz/

## Running it

Open `index.html` in any modern browser. It has no dependencies and needs no server or internet connection.

## Controls

| Button | What it does |
|---|---|
| **Shuffle** | Instantly rearranges the 40 items in a uniformly random order (Fisher–Yates). |
| **Displace** | Swaps one randomly chosen pair of neighbors in the current arrangement. Press repeatedly to make a nearly sorted list. |
| **Bubble** | Bubble sort that stops after a pass with no swaps. |
| **Bubble\*** | Bubble sort that also skips the settled tail. Each pass ends one item earlier. |
| **Selection** | Selection sort, swap version. |
| **Insertion** | Insertion sort. |
| **Pause / Resume** | Pauses the running sort after its current step, or resumes it. |
| **Speed** | Cycles the sort speed through 1x, 2x, 4x and 8x. Takes effect at the next step. |
| **Reset** | Stops the sort and restores the arrangement from just before it started. After a sort finishes, it restores the same starting arrangement, so the same data can be replayed with another algorithm or at another speed. |

The sort and data buttons are disabled while an animation runs. The button for the running algorithm stays highlighted.

## What the markers mean

- **Lifted item:** an item being moved or swapped. Half-lifted items are being examined (Insertion) or shifted aside to make room.
- **Dotted box (Bubble):** the pair of neighbors being compared.
- **Dotted vertical rule (Bubble\*):** items to the right are already in their final place and are no longer compared.
- **Dark dotted box (Selection):** the smallest item found so far in the current scan. It stays with that item until it is placed.
- **Faint dotted box (Selection):** the item currently being checked against the smallest so far.
- **Arrow (Selection):** the slot where the smallest item will be swapped to, i.e. the boundary between the sorted and unsorted parts.
- **Dotted box and full lift (Insertion):** the item being inserted (the "key").
- **Dotted vertical rule (Insertion):** the boundary between the sorted part (left) and the unsorted part (right).

## Where the visualization departs from textbook versions

These simplifications are deliberate, for clarity on screen.

1. **Insertion sort models a doubly linked list, not an array.** In the usual array version, larger items are shifted right one at a time *during* the leftward scan. Here the scan only examines items. Once the key's place is found, all larger items slide over together in a single step. This matches a doubly linked list, where inserting is a constant-time relink once the position is known. The backward scan is what requires the list to be *doubly* linked. The other three sorts are equally valid on such a list, so the whole demo can be read under this model.
2. **Animation time is not an exact cost model.** Comparisons take the same time on screen in all three algorithms, so comparison counts can be compared by eye. Swaps, slides, and the pick-up/put-down of the insertion key are timed for legibility, not to match their real relative costs. A swap of distant items (Selection) takes the same time whatever the distance, which is correct, since swapping is constant-time regardless of distance.
3. **Bubble sort variants.** Plain **Bubble** includes the early-exit check (stop when a pass makes no swaps) but compares the full list on every pass. **Bubble\*** adds the shrinking pass, which skips one more settled item per pass. It does not use the further refinement of skipping to the last swap position.
4. **Selection sort skips "swaps" of an item with itself.** When the smallest item is already in place, nothing moves.
5. **Stability is not shown.** All values are distinct (1–40), so the demo cannot show whether an algorithm keeps equal items in their original order. (The swap version of selection sort does not.)

## Customizing

Settings are at the top of the `<script>` in `index.html`:

- `N`: number of items (default 40).
- `DISPLACE_PAIRS`: neighbor swaps per Displace press (default 1).
- `SPEEDS`: the speed multipliers the Speed button cycles through.
- `T`: every animation duration and pause, grouped by button, in milliseconds.
- `verbose`: turns on console logging.

Colors, sizes, and lift heights are CSS variables at the top of the `<style>` block.
