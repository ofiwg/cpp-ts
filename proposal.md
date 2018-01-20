**Document number:**	Nnnnn=yy-nnnn
**Date:**	yyyy-mm-dd
**Project:** HPC Fabrics Proposal
**Reply-to:**	Your name and email address. List multiple authors if applicable. Obfuscate addresses like this: "Jane Proposer <jane at somewhere dot com>"

## Table of Contents

I. Introduction
II. Motivation and Scope
III. Impact on the Standard
IV. Design Decisions
V. Technical Specifications
VI. References
VII. Acknowledgements

## I. Introduction

In the fall of 2017, the Open Fabrics Working Group (OFIWG) discussed proposing an extention to the current version of the ISO C++
Networking Technical Specification (N4695) to include support for HPC Fabrics. The intent of this proposal is to improve the
programmability and accessibility of HPC interconnect hardware.

## II. Motivation and Scope

N4695 currently targets commodity, ethernet based, interconnects. Developing a fabric extension to N4695 will increase the accessibility
of fabric interconnects to HPC applications, runtimes, and languages. A fabric extension to the C++ Networking Technical Specification
will provide new mechanisms improving HPC application, runtime, and language performance and efficiencies.

## III. Impact On the Standard

The proposed fabric extension will depend on N4695. The proposed fabric extension is a "pure extension" of N4695. The current suite of
libraries used for HPC fabrics are implemented in C99. This proposed fabric extension can be implemented, at a minimum, using C++11
compilers and libraries.

## IV. Design Decisions

Design decisions in this proposal are presented as an extension to N4695. This proposal may impact N4695.

## V. Technical Specifications

## VI. References

## VII. Acknowledgements

This document is based on N4695, the ISO C++ Networking Technical Specification.

