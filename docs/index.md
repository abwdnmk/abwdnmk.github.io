### Problem Statement

You are given a string S*S* consisting of six types of characters: `(`, `)`, `[`, `]`, `<`, `>`.

A string T*T* is called a colorful bracket sequence if it satisfies the following condition:

> It is possible to turn T*T* into an empty string by repeating the following operation any number of times (possibly zero):
>
> - If there exists a contiguous substring of T*T* that is one of `()`, `[]`, or `<>`, choose one such substring and delete it.
> - If the deleted substring was at the beginning or end of T*T*, the remainder becomes the new T*T*.
> - Otherwise, concatenate the part before the deleted substring and the part after the deleted substring, and that becomes the new T*T*.

Determine whether S*S* is a colorful bracket sequence.