# Lab-6: Building Intuition for DNS

In this home lab, I will explore DNS by configuring and flushing the DNS for the Client-1 VM environment set up in previous labs. I will also document my findings and observations through the screenshots.

## A-Record Exercise

1. **Log into DC-1** as your domain admin account (`mydomain.com\jane_admin`).
2. **Log into Client-1** as an admin (`mydomain\jane_admin`).
3. From Client-1, try to **ping "mainframe"** and observe that it fails.
4. Run `nslookup "mainframe"` and notice that it fails (no DNS record exists).

![r1](https://github.com/user-attachments/assets/2507debe-9932-43d3-9136-cb94e40e90eb)

5. **Create a DNS A-record** on DC-1 for "mainframe" that points to DC-1's private IP address.

![r2](https://github.com/user-attachments/assets/b0234660-2d33-4509-8325-98128b75298b)

6. Return to **Client-1** and try to ping "mainframe" again. This time, it should succeed.

![r3](https://github.com/user-attachments/assets/030aca57-b1ad-4204-933e-94b74f354922)

## Local DNS Cache Exercise

7. On **DC-1**, change the mainframe's record address to `8.8.8.8`.

![r4](https://github.com/user-attachments/assets/b01f5e6f-b5cd-44d1-a25a-fb403c435ed4)

8. Go back to **Client-1** and ping "mainframe" again. Observe that it still pings the old address.

![r5](https://github.com/user-attachments/assets/2112f232-0bcc-425e-bc54-43c0490f9218)

9. Check the local DNS cache with the command `ipconfig /displaydns`.

![r6](https://github.com/user-attachments/assets/67d4fdc1-9861-45bc-9cb9-b894197c9ce5)

10. **Flush the DNS cache** using `ipconfig /flushdns`.
11. Verify the cache is empty using `ipconfig /displaydns`.
12. **Attempt to ping "mainframe"** again and observe that the new address (8.8.8.8) now shows up.

![r7](https://github.com/user-attachments/assets/68b00a94-178b-43b4-8444-0f7ca11623f8)

   After flushing the DNS, the new private IP address (8.8.8.8) appears, replacing the previous entry.

## CNAME Record Exercise

13. Go back to **DC-1** and create a CNAME record that points the host "search" to `www.google.com`.

![r8](https://github.com/user-attachments/assets/e0f8d84b-f107-4feb-9df1-6f516ebe86ca)

14. On **Client-1**, attempt to ping "search" and observe the result of the CNAME record.
15. Run `nslookup "search"` on Client-1 and observe the result of the CNAME record.

![r9](https://github.com/user-attachments/assets/f1fc62a3-95fc-45d1-b154-7d9ef04e3e8e)

The order of operations is as follows: Local DNS Cache > Local Host File > DNS Server.

---

## Key Takeaways

- **Configured DNS A-records**: Created an A-record in DNS and observed its effect on domain name resolution.
- **Understanding Local DNS Cache**: Explored how local DNS cache can retain old records and how to clear it using `ipconfig /flushdns`.
- **CNAME Record Implementation**: Created and tested a CNAME record, learning how it maps one hostname to another.
- **Troubleshooting with `nslookup`**: Used `nslookup` to query DNS records and troubleshoot DNS resolution.
- **DNS Resolution Hierarchy**: Gained an understanding of the DNS resolution order (Local DNS Cache > Host File > DNS Server).
- **Hands-on with DNS management**: Gained practical experience in managing DNS records and understanding DNS behavior in a cloud-based environment.

This project enhanced my understanding of DNS management, caching, and troubleshooting within a cloud-based environment, which is an essential skill for a Cloud Support Engineer.
