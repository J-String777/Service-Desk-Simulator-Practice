# Entry 02: Critical Hardware Failure and Replacement Deployment

- **Project:** Service Desk Simulator Practice
- **Ticket ID:** INC0012871
- **Ticket title:** Customer Support PC is completely dead, agent can't take calls
- **Category:** Hardware / Workstation Deployment
- **Priority:** Critical (the simulator also labels it Hard)
- **Status:** Resolved in simulation
- **Environment:** Service Desk Simulator (simulated environment only)

Screenshots are numbered 01 to 22 in the order I did things. Click any image to open it full size.

## 1. What the user reported

Quinn Adams, a Customer Support agent on Floor 1 (contact x2280), reported that his desktop would not turn on. He had already pressed the power button several times and checked the wall outlet with another device. The outlet worked, but the desktop showed no lights, no fan, and no beep.

Calls were piling up because he couldn't work without a functioning computer.

<p align="center"><img src="../screenshots/entry-02/01-ticket.png" width="720" alt="Original ticket INC0012871 with the reported issue and business impact"><br><sub><b>01.</b> The original ticket, still unassigned.</sub></p>

## 2. Initial assessment

I assigned the ticket to myself and reviewed Quinn's directory profile. I also contacted him through Company Chat. He had messaged at 4:52 PM because his manager asked him to follow up. At 4:56 PM I asked him three questions:

1. Is the power cable firmly connected at the back of the desktop and at the wall outlet or power strip?
2. Do you see any lights on the desktop or monitor, or is everything completely off?
3. Did anything unusual happen before this started, like a power outage or the computer shutting down unexpectedly?

Quinn answered that the power cable was connected at both ends, everything was completely off, and nothing unusual had happened beforehand. He asked for a replacement desktop because calls were piling up.

<table>
<tr>
<td align="center"><img src="../screenshots/entry-02/02-chat-follow-up.png" width="300" alt="Company Chat: Quinn's 4:52 PM follow-up and my 4:56 PM questions"><br><sub><b>02.</b> Quinn's follow-up and my questions. The simulator cut my message off after "calls are".</sub></td>
<td align="center"><img src="../screenshots/entry-02/03-chat-user-reply.png" width="300" alt="Company Chat: Quinn's reply that the cable is connected and everything is off"><br><sub><b>03.</b> Quinn's reply.</sub></td>
</tr>
</table>

At that point the exact hardware failure was unknown. The outlet worked, so power was reaching the wall, and a closer inspection of the desktop would normally come before declaring it unsalvageable or handing out a new one. But a Customer Support agent couldn't take calls, so I had to weigh the time needed to restore service against the time needed to diagnose the original computer.

## 3. Troubleshooting and decisions

**Step 1. Reviewed the symptoms.** The desktop had no signs of power, even though the wall outlet had been tested and the cable was connected at both ends.

**Step 2. Weighed the business impact and made a call.** This simulation is very open and lets you do the right or the wrong thing, so I looked up what to do in this case. Quinn couldn't take calls, so I decided to restore his ability to work quickly instead of spending the shift trying to repair a desktop that showed no signs of power. I looked at three tools: PC Shelf (where available replacement computers should be), Asset Management (identifying equipment and tracking assignments), and Computer Deployment (preparing or assigning a replacement).

**Step 3. Looked for an available replacement.** In Asset Management, filtered to Desktop, the visible rows were unassigned: SD2001 and SD2003 "Needs to be imaged", SD2011 "Broken", and SD2030 and SD2033 "Decommissioned". Ship Manager reported that no replacement PC was ready yet and pointed me to Computer Deployment to build one.

<p align="center"><img src="../screenshots/entry-02/04-asset-management.png" width="720" alt="Asset Management filtered to Desktop showing unassigned desktops and their statuses"><br><sub><b>04.</b> Asset Management, filtered to Desktop (13 of 639 assets).</sub></p>

<table>
<tr>
<td align="center"><img src="../screenshots/entry-02/05-computer-deployment.png" width="400" alt="Computer Deployment screen with Server Imaging, Manual Domain Enrollment and Cloud Provisioning"><br><sub><b>05.</b> Computer Deployment: Server Imaging, Manual Domain Enrollment, Cloud Provisioning (under development).</sub></td>
<td align="center"><img src="../screenshots/entry-02/06-ship-manager-no-pc.png" width="400" alt="Ship Manager showing no replacement PC is ready yet"><br><sub><b>06.</b> Ship Manager: no replacement PC ready yet.</sub></td>
</tr>
</table>

**Step 4. Chose the deployment method from the documentation.** I wasn't sure which setup a Customer Support PC needed, so I used the "Check the documentation" link and read "Choosing a PC Setup: Device Profiles & Deployment Methods" in Documentation Station. It says Server Imaging is for builds that need legacy software or on-prem device policy that the cloud can't deliver, and names the Customer Support softphone as the classic case. It also says Customer Support stays on Server Imaging even after the rollout. Manual Domain Enrollment is for shared Facilities kiosks and Engineering lab/test machines. I picked Server Imaging.

<p align="center"><img src="../screenshots/entry-02/07-docs-deployment-methods.png" width="720" alt="Documentation Station describing Server Imaging and Manual Domain Enrollment"><br><sub><b>07.</b> Documentation Station: when to use Server Imaging and Manual Domain Enrollment.</sub></p>

<p align="center"><img src="../screenshots/entry-02/08-docs-customer-support.png" width="720" alt="Documentation highlighting that Customer Support stays on Server Imaging"><br><sub><b>08.</b> The line I relied on (highlighted): Customer Support stays on Server Imaging.</sub></p>

**Step 5. Built the replacement with Server Imaging.** I followed the simulator's Server Imaging walkthrough:

   - **Physical setup.** Connected all five cables (power, Ethernet, DisplayPort, USB keyboard, USB mouse). The simulator showed 5/5 connected and "Ready to boot".
   - **Booting.** My first try missed the boot menu, so the workstation started its normal OS setup ("Missed the boot menu... Restart and try again"). I restarted and chose PXE Network Boot IPv4 in the Boot Manager.
   - **Task sequence.** In the Task Sequence Wizard the OSDCOMPUTERNAME variable was empty. The first tag I tried was already registered to an existing broken device, so I used the available tag SD2036 instead.
   - **Deployment.** The task sequence ran and joined the machine to the servicedesk-simulator.local domain. It reached the domain sign-in screen, and the simulator reported "Deployment Successful" for SD2036 (Server Imaging, Desktop).

<table>
<tr>
<td align="center"><img src="../screenshots/entry-02/09-physical-setup-start.png" width="400" alt="Physical setup with 0 of 5 cables connected"><br><sub><b>09.</b> Physical setup, 0/5 cables connected.</sub></td>
<td align="center"><img src="../screenshots/entry-02/10-physical-setup-done.png" width="400" alt="Physical setup with 5 of 5 cables connected, Ready to boot"><br><sub><b>10.</b> 5/5 connected, ready to boot (Step 3 of 11).</sub></td>
</tr>
</table>

<table>
<tr>
<td align="center"><img src="../screenshots/entry-02/11-missed-boot-menu.png" width="400" alt="Workstation OS Setup screen after missing the boot menu"><br><sub><b>11.</b> First try: I missed the boot menu (Step 4 of 11).</sub></td>
<td align="center"><img src="../screenshots/entry-02/12-boot-manager-pxe.png" width="400" alt="Boot Manager with PXE Network Boot IPv4 selected"><br><sub><b>12.</b> Second try: PXE Network Boot IPv4 in the Boot Manager.</sub></td>
</tr>
</table>

<table>
<tr>
<td align="center"><img src="../screenshots/entry-02/13-task-sequence-variables.png" width="400" alt="Task Sequence Wizard with an empty OSDCOMPUTERNAME value"><br><sub><b>13.</b> Task Sequence Wizard: OSDCOMPUTERNAME is empty (Step 8 of 11).</sub></td>
<td align="center"><img src="../screenshots/entry-02/14-edit-variable.png" width="400" alt="Edit Variable dialog for OSDCOMPUTERNAME"><br><sub><b>14.</b> Editing the variable.</sub></td>
</tr>
</table>

<table>
<tr>
<td align="center"><img src="../screenshots/entry-02/15-computer-name-sd2036.png" width="400" alt="OSDCOMPUTERNAME set to SD2036"><br><sub><b>15.</b> OSDCOMPUTERNAME set to SD2036.</sub></td>
<td align="center"><img src="../screenshots/entry-02/16-join-domain.png" width="400" alt="Installation progress: Join Domain servicedesk-simulator.local"><br><sub><b>16.</b> Task sequence running: Join Domain (Step 9 of 11).</sub></td>
</tr>
</table>

<table>
<tr>
<td align="center"><img src="../screenshots/entry-02/17-domain-sign-in.png" width="400" alt="Domain sign-in screen on the new workstation"><br><sub><b>17.</b> Domain sign-in screen on the new workstation.</sub></td>
<td align="center"><img src="../screenshots/entry-02/18-deployment-successful.png" width="400" alt="Deployment Successful for SD2036, Server Imaging, Desktop"><br><sub><b>18.</b> Deployment Successful: SD2036, Server Imaging, Desktop.</sub></td>
</tr>
</table>

**Step 6. Found the finished PC on the PC Shelf.** SD2036 showed up as a Server Imaging build with "1 ready to ship".

<p align="center"><img src="../screenshots/entry-02/19-pc-shelf.png" width="480" alt="PC Shelf showing SD2036 ready to ship"><br><sub><b>19.</b> PC Shelf: SD2036, 1 ready to ship.</sub></p>

**Step 7. Arranged the shipment.** In Ship Manager I set the recipient to Quinn Adams, the sender to IT Department, and the reference to INC0012871. I selected desktop SD2036 and chose Rush Priority (Instant) with a return label. Quinn works on site, and the "Where Replacements Ship" section of the same documentation article says equipment for on-site employees goes to the site receiving dock and never to a home address. So I entered the dock address from the documentation: 1200 Commerce Park Drive, Columbus, OH 43215.

<p align="center"><img src="../screenshots/entry-02/20-ship-manager-opened.png" width="720" alt="Ship Manager opened next to the ticket, with one computer available to ship"><br><sub><b>20.</b> Ship Manager now shows one computer available (before filling it in). The assignee name is hidden.</sub></p>

<p align="center"><img src="../screenshots/entry-02/21-ship-manager-completed.png" width="720" alt="Completed Ship Manager form for SD2036 to Quinn Adams with Rush Priority and a return label"><br><sub><b>21.</b> The completed shipment: SD2036, Rush Priority (Instant), return label included.</sub></p>

## 4. Resolution and verification

Quinn later messaged me that the replacement had already arrived, that he had plugged it in, and that it was working perfectly.

<p align="center"><img src="../screenshots/entry-02/22-user-confirmation.png" width="320" alt="Company Chat: Quinn confirms the replacement arrived and works"><br><sub><b>22.</b> Quinn confirms the replacement arrived and works.</sub></p>

This confirmed that the replacement computer powered on successfully. The original desktop's hardware fault was not diagnosed during this ticket.

## 5. Knowledge base notes

- Customer Support replacements need Server Imaging because of the department's legacy softphone and on-prem policy requirements.
- Before deploying equipment, check Asset Management for existing asset tags and use an available one.
- For an on-site employee, ship to the documented receiving dock, not a home address. (Someone who works from home gets the delivery address they give you.)
- A successful shipment isn't enough by itself to verify that service is restored. Follow up with the user and record their actual confirmation.

## 6. What I learned

Resolving an incident isn't always about repairing the original device. When a computer is completely unresponsive and the problem is stopping someone from doing their job, it can make sense to prioritize a replacement while documenting what's still unknown.

I also learned to check asset records before assigning a tag and to follow the deployment requirements for the user's department. The most important last step was following up with Quinn instead of assuming the shipment alone solved the problem.

## 7. Limitations

This was a simulated service desk ticket, not a real production incident. I didn't identify the original desktop's failed component. Quinn's message confirmed that the replacement was working, but it didn't independently establish whether he had gone back to taking calls.
