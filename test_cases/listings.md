Listings – Test Cases

Functional
1. Create listing (owner)
   - Input: valid payload
   - Expect: 201, listing_id
2. Create listing (tenant)
   - Expect: 403
3. Get listings with filters
   - Input: city, rent range, pagination
   - Expect: 200, results constrained, metadata
4. Update listing (owner)
   - Expect: 200; changes persisted
5. Delete listing (non-owner)
   - Expect: 403

Edge
6. Oversized photos
   - Expect: 413 or validation error
7. SQL injection-like inputs
   - Expect: 400; no crash

Performance
8. p95 < 300ms for list fetch with indexes


