# get_customer_details

Returns full details for a single customer by their **external ID** (`customerId`). The customerId is the customer's unique identifier in the client's system (their user ID, email, or phone).

## What's included

- Profile: name, email, mobile, gender, DOB
- Referral: code, link, status
- Custom attributes
- Tags
- UTMs
- Devices
- Payment methods
- Total spent
- Last order date

## User prompting

If the user asks for customer details without providing an ID, ask them for the customer's external ID. Present the results in a friendly summary — highlight key info like name, tier, points balance, and tags rather than dumping raw data.

## Notes

- Use the `externalId` from `get_customers` (NOT the Gameball numeric `id`).
- For tag-management tools (`assign_customer_tags`, `remove_customer_tags`), use the Gameball numeric `id` instead.
