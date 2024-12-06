# Lab-6: Building Intuition for DNS

In this home lab, I will explore DNS by configuring and flushing the DNS for the Client-1 VM environment set up in previous labs. I will also document my findings and observations through the screenshots.

## A-Record Exercise

1. **Log into DC-1** as your domain admin account (`mydomain.com\jane_admin`).
2. **Log into Client-1** as an admin (`mydomain\jane_admin`).
3. From Client-1, try to **ping "mainframe"** and observe that it fails.
4. Run `nslookup "mainframe"` and notice that it fails (no DNS record exists).

   ![image](https://github.com/user-attachments/assets/1c142881-9e70-42ce-8eff-9a44ad570fdd)

5. **Create a DNS A-record** on DC-1 for "mainframe" that points to DC-1's private IP address.

   ![image](https://github.com/user-attachments/assets/2a167ea5-4e95-4b05-98af-346192aeebd8)

6. Return to **Client-1** and try to ping "mainframe" again. This time, it should succeed.

   ![image](https://github.com/user-attachments/assets/7cc3cbb4-7ce7-4a2c-91fc-87efb828b0ca)

## Local DNS Cache Exercise

7. On **DC-1**, change the mainframe's record address to `8.8.8.8`.

   ![image](https://github.com/user-attachments/assets/84296ff6-b388-4fd4-aae8-14f2ec3cfabb)

8. Go back to **Client-1** and ping "mainframe" again. Observe that it still pings the old address.

   ![image](https://github.com/user-attachments/assets/50a09d29-f37e-4b96-8512-bc0e4d5085b8)

9. Check the local DNS cache with the command `ipconfig /displaydns`.

   ![image](https://github.com/user-attachments/assets/2e2aa513-b23d-4bac-acb1-448b33c41fca)

10. **Flush the DNS cache** using `ipconfig /flushdns`.
11. Verify the cache is empty using `ipconfig /displaydns`.
12. **Attempt to ping "mainframe"** again and observe that the new address (8.8.8.8) now shows up.

   ![image](https://github.com/user-attachments/assets/a244e852-42db-4855-8b8f-9443b6525104)

   After flushing the DNS, the new private IP address (8.8.8.8) appears, replacing the previous entry.

## CNAME Record Exercise

13. Go back to **DC-1** and create a CNAME record that points the host "search" to `www.google.com`.

   ![image](https://github.com/user-attachments/assets/1dc60c25-e8ab-426f-a912-dc93a6302de4)

14. On **Client-1**, attempt to ping "search" and observe the result of the CNAME record.
15. Run `nslookup "search"` on Client-1 and observe the result of the CNAME record.

   ![image](https://github.com/user-attachments/assets/74727f38-0d83-4b5a-aa4d-f8decfa3e16b)

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
