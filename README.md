# Project Idea: StarkParking

## Introduction

StarkParking is a parking application built on the Starknet platform, allowing users to reserve spots and make payments using the `STRK` token. The application will store all related data, including parking lots, bookings, and parking times, on the blockchain to ensure transparency and security.

## Key Features

### 1. Parking Lot Registration

- Users can register parking lots by paying a fee, which will be refunded after a specified period.
- The creator must provide a wallet address for receiving `STRK` tokens when drivers make payments.

### 2. Parking Spot Reservation

- Users can select a parking lot and slot, then record their entry time.
- The system will check the slot status before allowing reservations.

### 3. Service Fee Calculation

- Prices will be set in `cents (USD)` and pegged to the value of `USDT`.
- An oracle will be used to convert the price from USD to the equivalent amount in `STRK`.

### 4. Data Storage

- All information about parking lots and bookings will be stored on the blockchain to ensure transparency and security.

## Data Structures

### 1. Parking Lot Data Structure

```rust
struct ParkingLot {
  lot_id: u256,
  name: felt252,
  location: felt252,
  slot_count: u32,
  price_per_hour_usd: u64,
  creator: ContractAddress,
  wallet_address: ContractAddress,
  registration_time: u256
}
```

### 2. Booking Data Structure

```rust
struct Booking {
  booking_id: felt252,
  lot_id: u256,
  slot: u8,
  entry_time: u256,
  exit_time: u256,
  total_payment: u64,
  payer: ContractAddress
}
```

### Define the Storage

```rust
#[storage]
struct Storage {
  #[substorage(v0)]
  ownable: OwnableComponent::Storage,
  parking_lots: Map::<u256, ParkingLot>, // Mapping from lot_id to ParkingLot
  bookings: Map::<felt252, Booking>, // Mapping from booking_id to Booking
  available_slots: Map::<u256, u32>, // Mapping from lot_id to available slots
  payment_token: ContractAddress,
  ...
}
```
