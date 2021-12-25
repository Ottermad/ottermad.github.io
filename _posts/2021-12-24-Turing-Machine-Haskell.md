---
layout: post
title: Writing a Turing Machine in Haskell
author: Charles Thomas
---

As I've been learning Quantum Computing, I've had to learn some Computer Science along the way. One of the concepts I'd heard of but I hadn't understood until recently was that of a Turing Machine.

To understand what a Turing Machine was I decided to write one in Haskell.

# Setting up the project
* Install Haskell
* Create the file structure
* Setup the .cabal file

# Modelling the machine

## State
The first thing a Turing Machine has is a series of states it can move between. In our case, are two special states we need to make a note of:
* The start state which is the state it starts in
* The halt state which is the state it finishes in

We are going to represent these and 3 other generic states with the following line:

```haskell
data State = Halt | StartState | A | B | C deriving (Eq, Show)
```

## The Tape
The next thing a Turing machine has is a tape and on each square on the tape is a symbol. Let's represent this as:

```haskell
data Symbol = Start | Zero | One | Blank deriving (Eq, Show)
type Tape = [Symbol]
```

## Instructions
A Turing machine also has a list of instructions. In a Turing Machine, the instructions have 5 main parts.

The first two parts of instructions are  a symbol and a state. They are used to work out if we should apply an instruction . If the current state of the Turing machine and the current symbol on the tape match these two, then the instruction is applied. 

The three parts of instructions are used when that instruction applied. It is a new state to put the machine into, it is a new symbol to write to the current position on a tape, and finally an indication whether to move the tape forward a square, back a square or to keep it in the same place.

```haskell
data PositionShift = Backwards | Forwards | Stay deriving (Show)

data Instruction = Instruction { 
    stateToMatch :: State, 
    symbolToMatch :: Symbol, 
    newState :: State, 
    newSymbol :: Symbol, 
    positionShift :: PositionShift 
} deriving (Show)
```

## The Machine
Now we can represent the turing machine itself. We need to keep track of it all the states it could be in, its current state, the tape and the current position on the tape and the instructions.

```haskell
data TuringMachine = TuringMachine { 
    states :: [State], 
    currentState :: State, 
    tape :: Tape, 
    currentPosition :: Int, 
    instructions :: [Instruction] 
} deriving (Show)
```

# The Logic
So the first part of the logic of our turing machine, is to look at its current state, if its in halted state we end but if not we try and see if there is an instruction we can process.

```haskell
runMachine :: TuringMachine -> TuringMachine
runMachine machine
    | (currentState machine) == Halt = machine
    | otherwise  = runMachine (machineCycle machine)
```

Here the `machineCycle` is responsible for trying to find a instruction to run, if it finds one, it runs it, otherwise it sets the machine to the Halt state.

```haskell
machineCycle :: TuringMachine -> TuringMachine
machineCycle machine = 
    case instructionToApply of 
        Just instruction -> applyInstruction machine instruction
        Nothing -> haltMachine machine
    where instructionToApply = findInstructionToApply machine (instructions machine)

haltMachine :: TuringMachine -> TuringMachine
haltMachine machine =
    TuringMachine {
        states = states machine, 
        currentState = Halt, 
        tape = tape machine, 
        currentPosition = currentPosition machine,
        instructions = instructions machine
    }
```

## Looking for an instruction
To find an instruction to apply it recursively searches the list of instructions:
```haskell
findInstructionToApply :: TuringMachine -> [Instruction] -> Maybe Instruction
findInstructionToApply machine instructions
    | null instructions = Nothing
    | shouldApplyInstruction machine (instructions !! 0) =  Just (instructions !! 0)
    | otherwise = findInstructionToApply machine (tail instructions)
```

If the instructions array is empty it returns 0, otherwise it checks the first instruction in the list. If it should be applied it returns it. Otherwise it calls itself with the remaining instructions.

To determine an instruction should be applied we use this function that compares the current state and symbol of the machine to the instruction
```haskell
shouldApplyInstruction :: TuringMachine -> Instruction -> Bool
shouldApplyInstruction machine instruction = 
    (currentState machine == stateToMatch instruction) && (currentSymbol machine == symbolToMatch instruction)

currentSymbol :: TuringMachine -> Symbol
currentSymbol machine = (tape machine) !! (currentPosition machine)
```

## Applying an instruction
Now we need a function to apply the instruction when we've found one:

```haskell
applyInstruction :: TuringMachine -> Instruction -> TuringMachine
applyInstruction machine instruction =
    TuringMachine {
        states =  states machine, 
        currentState = newState instruction, 
        tape = newTape (tape machine) (currentPosition machine) (newSymbol instruction), 
        currentPosition = getNewPosition (machine) (positionShift instruction),
        instructions = instructions machine
    }

-- Given a tape, a position in the tape to update and a symbol it creates a new tape
newTape :: Tape -> Int -> Symbol -> Tape
newTape tape position newSymbol =
    take (position) tape ++ newSymbol : drop (position+1) tape

-- This takes a position and a shift and returns a new position
getNewPosition :: TuringMachine -> PositionShift -> Int
getNewPosition machine Forwards = (currentPosition machine) + 1
getNewPosition machine Stay = (currentPosition machine)
getNewPosition machine Backwards 
    | (currentPosition machine) == 0 = 0
    | otherwise = (currentPosition machine) - 1
```

## Creating a new machine
Finally, we have a helper that creates a new Turing with an infinite tape:
```haskell
newTuringMachine :: Tape -> [Instruction] -> TuringMachine 
newTuringMachine tape instructions = TuringMachine{
        states = [Halt, StartState, A, B, C],
        currentState = StartState,
        tape = [Start] ++ tape ++ repeat Blank,
        currentPosition = 0,
        instructions = instructions
    }

```

# Testing it
We can create a test by creating a machine that always outputs one:
```haskell
module TuringSpec (spec) where

import Turing
import Test.Hspec

spec :: Spec
spec = do
    describe "Turing Machine" $ do
        it "always writes one" $ do
            tape (runMachine (newTuringMachine [One, Zero, One] [
                    Instruction{stateToMatch = StartState, symbolToMatch=Start, newState = A, newSymbol = Start, positionShift = Forwards},
                    Instruction{stateToMatch = A, symbolToMatch=Zero, newState = A, newSymbol = Blank, positionShift = Forwards},
                    Instruction{stateToMatch = A, symbolToMatch=One, newState = A, newSymbol = Blank, positionShift = Forwards},
                    Instruction{stateToMatch = A, symbolToMatch=Blank, newState = B, newSymbol = Blank, positionShift = Backwards},
                    Instruction{stateToMatch = B, symbolToMatch=Blank, newState = B, newSymbol = Blank, positionShift = Backwards},
                    Instruction{stateToMatch = B, symbolToMatch=Start, newState = C, newSymbol = Start, positionShift = Forwards},
                    Instruction{stateToMatch = C, symbolToMatch=Blank, newState = Halt, newSymbol = One, positionShift = Stay}
                ]
                )) !! 1 == One
```