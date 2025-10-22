# 🧩 Kustomize Patching Configurations

This walkthrough demonstrates how to identify, inspect, and modify Kubernetes resources using **Strategic Merge Patches** and **Inline JSON patches** with Kustomize.

---

## 📂 Folder Structure

Each directory contains its own `kustomization.yaml` file and patch definitions.

<br><br>

<p align="center">
  <img width="257" height="152" alt="folder tree" src="https://github.com/user-attachments/assets/4693daab-e806-4b75-a3b6-b899394bd179" />
</p>

---

## 🧠 Step 1 – How Many Containers Are in This Deployment?

At first glance, the deployment YAML might look like it has a single container.  
But let’s confirm that by checking if any **patches** are applied.

<br><br>

<p align="center">
  <img width="208" height="278" alt="deployment yaml" src="https://github.com/user-attachments/assets/fdef7bf5-2578-4420-9f2e-32f1d010f69a" />
</p>

<br><br>

Checking the `kustomization.yaml` reveals a related patch:

<br><br>

<p align="center">
  <img width="190" height="168" alt="kustomization patch reference" src="https://github.com/user-attachments/assets/10646a63-47c3-4ec1-a22d-a7954c9cbad1" />
</p>

<br><br>

Let’s inspect the patch file itself:

<br><br>

<p align="center">
  <img width="175" height="155" alt="patch adds container" src="https://github.com/user-attachments/assets/594e9cf8-c48e-42c9-967c-3b2356462fe5" />
</p>

✅ **Answer:** The patch adds another container — so the deployment now has **2 containers**.

---

## 📦 Step 2 – Does the Deployment Have a Volume?

Let’s inspect whether a **volume** is defined — or added through a patch.

<br><br>

<p align="center">
  <img width="159" height="255" alt="check volume" src="https://github.com/user-attachments/assets/55b5ccdc-bcdb-492a-8af4-a741ba8b1419" />
</p>

<br><br>

Checking for patches again:

<br><br>

<p align="center">
  <img width="190" height="161" alt="volume patch reference" src="https://github.com/user-attachments/assets/b45506f7-fb40-41a0-9ede-eba9bb0eda93" />
</p>

<br><br>

Looks like we found it — a patch that adds a volume definition:

<br><br>

<p align="center">
  <img width="239" height="241" alt="volume patch" src="https://github.com/user-attachments/assets/3953963d-95dd-488b-887c-df48ed42cf5e" />
</p>

---

## ⚙️ Step 3 – Confirm the Applied Build

After running the Kustomize build, we can confirm the patch was applied successfully —  
the deployment now has **two containers**.

<br><br>

<p align="center">
  <img width="219" height="297" alt="two containers" src="https://github.com/user-attachments/assets/07637160-3f30-4158-b85e-57108b0b3899" />
</p>

---

## ✂️ Step 4 – Create a Strategic Merge Patch to Remove the Second Container

We’ll now remove one container using a **Strategic Merge Patch**.

1. Copy the relevant parts of the original deployment into a new patch file.
2. Keep only the metadata and the specific fields you want to modify.

<br><br>

<p align="center">
  <img width="175" height="288" alt="copy deployment to patch" src="https://github.com/user-attachments/assets/ccc7eb2a-f4fe-424c-b96d-71a683db9db8" />
</p>

<br><br>

<p align="center">
  <img width="186" height="150" alt="minimal patch" src="https://github.com/user-attachments/assets/e215b128-909f-4247-b7e1-fc36d5d7a23b" />
</p>

<br><br>

Add the patch to your `kustomization.yaml`:

<br><br>

<p align="center">
  <img width="166" height="116" alt="kustomization edit" src="https://github.com/user-attachments/assets/29915905-88f7-4dfb-8e3b-d2a661f7b27f" />
</p>

<br><br>

Build again — success! The second container was removed.

<br><br>

<p align="center">
  <img width="937" height="83" alt="build success" src="https://github.com/user-attachments/assets/ede8c4a2-3acb-45c2-aeb4-dfd265b09dd3" />
</p>

---

## 🧾 Step 5 – Apply an Inline JSON Patch

Now we’ll use an **inline JSON patch** directly inside the `kustomization.yaml`.

JSON patches are great for small, targeted edits without creating a separate file.

<br><br>

<p align="center">
  <img width="333" height="193" alt="json patch" src="https://github.com/user-attachments/assets/9aebceb2-e935-42aa-9633-60649ed127a0" />
</p>

---

## 🚀 Step 6 – Build, Apply, and Verify

Run the Kustomize build again to apply all changes.

<br><br>

<p align="center">
  <img width="423" height="58" alt="build command" src="https://github.com/user-attachments/assets/3d743d89-8eb7-47f2-9858-c081f6f07354" />
</p>

<br><br>

Check that the labels are updated and everything looks correct:

<br><br>

<p align="center">
  <img width="706" height="69" alt="final labels" src="https://github.com/user-attachments/assets/b8351ff5-e7b6-4002-8ef5-efc0d9c88a41" />
</p>

✅ **Done!** You’ve successfully:
- Added and removed containers using **Strategic Merge Patches**  
- Modified configuration inline with **JSON patches**  
- Verified the results through **Kustomize build**

---

## 🧠 Key Takeaways

- **Strategic Merge Patches** are ideal for YAML-level structural edits (add/remove/update).  
- **JSON Patches** are perfect for precise, inline tweaks.  
- Both approaches maintain clean, version-controlled YAMLs — no need to modify base manifests.  
- Together, they make **Kustomize** a powerful and declarative configuration management tool.

---
