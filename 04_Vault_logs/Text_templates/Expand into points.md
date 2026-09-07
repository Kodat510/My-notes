---
name: 3 points
description: Summarises the explanation into as many points as required
author: Kodat510
version: 1.0.0
---
Summarize the entire input into clear, bite-sized points while preserving ALL meaningful information.

Your goal is NOT to shorten the content aggressively. Your goal is to make the information easier to review without losing meaning, context, reasoning, examples, distinctions, conclusions, important details, or insights.

## Core Rules

1. Preserve every important idea from the original.
    
2. Break large ideas into small, independently understandable bullet points.
    
3. Use simple, precise language.
    
4. Preserve the original meaning and intent.
    
5. Do not introduce new claims, interpretations, or information.
    
6. Do not omit:
    
    - explanations
        
    - reasoning
        
    - examples
        
    - definitions
        
    - distinctions
        
    - cause-and-effect relationships
        
    - qualifications or exceptions
        
    - conclusions
        
    - uncertainties
        
    - questions raised by the original
        
    - meaningful personal observations
        
7. If several sentences express one connected idea, combine them into one concise point rather than repeating them.
    
8. If one sentence contains several distinct ideas, split them into separate points.
    
9. Preserve technical terminology when it carries meaning.
    
10. Explain technical terminology briefly when necessary for understanding.
    
11. Do not replace specific information with vague statements.
    
12. Do not give opinions about the input.
    
13. Do not evaluate whether the ideas are correct unless the input itself does so.
    
14. Preserve the hierarchy of ideas:
    
    - Main concept
        
        - Supporting idea
            
        - Example
            
        - Consequence
            
15. When the original compares two or more things, explicitly preserve the comparison.
    
16. When the original describes a process, preserve the sequence of steps.
    
17. When the original contains a definition, make it explicit.
    
18. When the original contains an insight or realization, preserve it as an insight rather than reducing it to a generic fact.
    
19. Remove conversational filler, repetition, and wording that adds no information.
    
20. Make the final result substantially easier to scan and revise than the original while retaining essentially all of its information.
    

## LaTeX and Mathematical Formatting

Use LaTeX whenever it is suitable, especially for:

- equations
    
- mathematical expressions
    
- variables
    
- vectors
    
- matrices
    
- functions
    
- derivatives
    
- integrals
    
- summations
    
- Greek letters
    
- units or relationships where mathematical notation improves clarity
    

This output is going directly into Obsidian.

For ALL LaTeX, use Obsidian-compatible `$$` delimiters.

For standalone equations, use:

equationequation

For example:

Av=λvA\mathbf{v} = \lambda\mathbf{v}

and:

det⁡(A−λI)=0\det(A-\lambda I)=0

Do NOT use `\[ \]` delimiters.

Do NOT use `\(...\)` delimiters.

For short mathematical expressions inside a sentence, still use `$$...$$` because the output must consistently use `$$` tags for Obsidian.

For example:

- An eigenvector satisfies Av=λvA\mathbf{v}=\lambda\mathbf{v}.
    
- The eigenvalue is the scaling factor λ\lambda.
    
- The characteristic equation is obtained from det⁡(A−λI)=0\det(A-\lambda I)=0.
    

Preserve equations from the original accurately. Do not alter mathematical notation unless necessary to correct obvious formatting.

## Code and Technical Formatting

Use Markdown code blocks for code.

Use inline code formatting for:

- function names
    
- variable names
    
- commands
    
- file names
    
- package names
    
- API names
    
- programming constructs
    

Preserve code exactly when the original contains code, unless only formatting changes are necessary.

## Structure

Use the following structure when appropriate:

# Summary

## Main Idea

- ...
    

## Key Concepts

- ...
    
- ...
    
    - ...
        
    - ...
        

## Important Details

- ...
    
- ...
    

## Examples / Applications

- ...
    

## Conclusions / Insights

- ...
    

Only include sections that are actually supported by the input.

Do not force information into categories that do not fit.

## Critical Principle

Think of this as "lossless compression of understanding," not ordinary summarization.

The purpose is to transform my raw notes into a compact representation that allows me to reconstruct the original understanding later.

If removing a sentence would cause me to lose information necessary to reconstruct the original meaning, KEEP that information.

Compress wording, not knowledge.