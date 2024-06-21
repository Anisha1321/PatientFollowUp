# PatientFollowUp
Patient Follow Up Smart Contract using solidity
# PatientFollowUp Smart Contract

## Overview

The `PatientFollowUp` smart contract is designed to manage and track follow-up appointments for patients using the Ethereum blockchain. This contract allows the addition of new patients, the recording of follow-up appointments, the retrieval of patient details, and the verification of data integrity through invariant checks.

## Prerequisites

To work with this contract, you'll need:
- Solidity version 0.8.26
- An Ethereum development environment (such as Remix, Truffle, or Hardhat)

## Contract Details

### Patient Structure

The contract defines a `Patient` structure to store patient information. Each `Patient` includes a `name` (string) to identify the patient, an `age` (uint256) to record the patient's age, an `exists` (bool) flag to check the patient's presence in the system, a `followUpCount` (uint256) to keep track of the number of follow-up appointments, and a `lastFollowUpDate` (uint256) to store the date of the last follow-up.

### Functions

#### `addPatient`

The `addPatient` function is designed to add a new patient to the system. It takes the patient's Ethereum address, name, and age as parameters. The function starts by ensuring the patient does not already exist in the system using the `require` statement to check the `exists` field in the `patients` mapping. If the patient already exists, it reverts with the message "Patient already exists." It also validates that the provided age is greater than zero to ensure valid age data. Upon passing these checks, a new `Patient` struct is created and stored in the `patients` mapping, initialized with the provided name and age, and default values for `followUpCount` and `lastFollowUpDate`. The patient's address is then added to the `patientAddresses` array for tracking. This function is essential for onboarding new patients into the follow-up tracking system.

#### `recordFollowUp`

The `recordFollowUp` function records a follow-up appointment for an existing patient. It accepts the patient's Ethereum address and the follow-up date as parameters. The function starts by ensuring the patient exists in the system using a `require` statement. If the patient does not exist, it reverts with the message "Patient does not exist." It also checks that the follow-up date is in the future using another `require` statement. If the follow-up date is not in the future, it reverts with the message "Follow up date must be in future." Upon passing these checks, the function retrieves the patient's record from the `patients` mapping, increments the `followUpCount`, and updates the `lastFollowUpDate` with the provided date. This function is critical for maintaining accurate and up-to-date records of patient follow-ups.

#### `getDetails`

The `getDetails` function retrieves detailed information about a specific patient. It takes the patient's Ethereum address as a parameter and starts by checking if the patient exists using an `if` statement. If the patient does not exist, it reverts with the message "Patient does not exist." If the patient exists, the function retrieves the patient's data from the `patients` mapping and returns their name, age, follow-up count, and last follow-up date. This function provides an efficient way to access important patient information, making it useful for administrators and users who need to view patient details.

#### `checkInvariant`

The `checkInvariant` function verifies an important invariant of the contract to ensure data integrity. It calculates the total number of follow-ups by iterating through all patient addresses stored in the `patientAddresses` array and summing their `followUpCount` values. After calculating the total follow-ups, the function uses an `assert` statement to check that the total number of follow-ups is non-negative. This invariant check helps maintain the correctness of the contract by ensuring that the total follow-up count cannot be negative, which would be logically inconsistent. Including this function allows the contract to perform a self-check to confirm that the data it stores remains valid and consistent over time.
