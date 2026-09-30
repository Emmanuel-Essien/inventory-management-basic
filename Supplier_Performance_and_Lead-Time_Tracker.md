# F/ND/25/3210039
# Feature 1 
# Feature Name: 
  Supplier Performance and Lead-Time Tracker
# ​Description: 
  A tracking feature that monitors past supplier delivery timelines and automatically adjusts reordering schedules if a vendor consistently delivers late.
# ​Purpose: 
  To factor real-world supply chain bottlenecks into the reordering timeline before stock runs out.
# ​How It Works: 
  It logs the date a purchase order was placed versus the date goods were actually received, calculating an average delay variance for each vendor.
# ​Information Required: 
  Purchase order creation date, expected delivery date, actual goods receipt date, and vendor ID.
# ​Output / Action: 
  Automatically extends the lead-time parameter for specific vendors and triggers earlier reorder warnings to compensate for expected delays.
# ​Benefits: 
  Prevents unexpected stockouts caused by slow suppliers and improves vendor accountability.
# ​Limitations / Dependencies: 
  Requires staff to accurately log goods receipt dates immediately upon delivery arrival.
# ​Sources: 
  Supply Chain Management Best Practices
