## Building AOSP with foss.crave.io and its devspace

**Are AOSP build times slowing you down?**

crave.io can significantly accelerate your Android Open Source Project (AOSP) builds. This developer productivity platform cuts build times from hours to minutes, freeing you to focus on coding and innovation.

**Key benefits:**

- **Faster builds:** See your changes reflected in minutes, not hours.
- **Streamlined workflow:** Build AOSP using your preferred IDE and tools.
- **Reduced complexity:** No need to manage build dependencies or infrastructure.

**Getting started with crave.io is easy:**

1. **Sign Up:** Join the crave.io [**Discord server**](https://discord.gg/EJxksGJEBS).
2. **Join Team AOSP:** Join Discord, then ask for team access in channel #ext-foss-aosp.
3. **Explore (Optional):** For potentially easier setup, explore [**crave_aosp_builder**](https://github.com/sounddrill31/crave_aosp_builder.git).

**All done? Got access to the foss.crave.io account? Let's get started with how to access devspace locally:**

1. **Getting crave conf file:** It is very easy. Navigate to the [**API Keys**](https://foss.crave.io/app/#/apikeys) tab and download the key that was auto-generated for you.
2. **Setup cmd:** To get the crave-command-line tool, navigate to the [**Downloads**](https://foss.crave.io/app/#/downloads) tab and download the binary for your platform, saving it as "crave" somewhere in your $PATH.

**Want to use it from a cloud server? It can be your own or [segfault](https://www.thc.org/segfault/):**

1. **For shell:** If you want to use segfault in the browser, you can continue with [**segfault shell**](https://shell.segfault.net/). Also, make sure to save the SECRET given to you.
2. **For SSH:**

   - If you want to use segfault through [**shell**](https://en.wikipedia.org/wiki/Secure_Shell), then do ```ssh root@segfault.net```. The password is 'segfault'.
   - After a few seconds, you'll be greeted with some messages; you can explore them, but for now, save the SSH line with the SECRET key. Here's an [**example**](./examples/segfault).

3. **Setup cmd:**

   - Now that you have access to the segfault server, let's set up the crave-command-line tool.  

   ```
   sudo apt-get update
   sudo bash -c "$(curl -fsSL https://github.com/accupara/crave/raw/master/get_crave.sh)"
   ```


**Let's join devspace:**

- Download or manually copy your crave.conf file from the [**API Keys**](https://foss.crave.io/app/#/apikeys) tab.
- To save the config manually, copy the contents of crave.conf and paste it into your segfault server using ```nano crave.conf```.
- Here's an example [**crave.conf**](./examples/crave.conf) file.
- Go to the directory where the crave.conf file is located (it can be Downloads).
- Inside that folder, run this command to log into your devspace.

   ```
   crave -c ./crave.conf devspace
   ```
- Boom! It's that easy.

**Clone project:**

1. We entered devspace successfully, let's build any ROM we want. For now, let's build LineageOS.

- First, you have to clone the LineageOS project into your devspace.
- For that, you need to do ```crave clone list```.
- It will list all existing project lists. You can clone anything you want, but for now, let's clone the LineageOS project.
  
   ```
   crave clone create --projectID 72 lineageos
   ```
- You will find the project ID in those lists, and the "lineageos" after the project ID stands for the directory you want to clone.

**Let's build:**

1. Cloned successfully? Let's start building.
2. **No matter what, don't build inside the devspace.**
3. To start the build, you need to follow this method, or you can have your own build script like this.
 
```
crave run --no-patch -- "repo init -u https://github.com/LineageOS/android.git -b lineage-21.0 --git-lfs --depth=1 
git clone https://github.com/username/local_manifest --depth 1 -b branch .repo/local_manifests && 

# Sync the repositories
/opt/crave/resync.sh  && 

# Set up build environment
source build/envsetup.sh && 
 
# Build the ROM
lunch lineage_codename-ap1a-variant && make installclean && mka bacon"
```

4. Boom! Your queue started. When your build starts, you can check logs here and also inside the foss.crave.io web interface.
5. I would recommend using either ```tmux``` or ```screen``` to not kill your running session.

**Sync different ROM:**

1. In case you want to build a different ROM, it's really simple. Here's one example.

```
crave run --no-patch -- "repo init -u https://github.com/RisingTechOSS/android.git -b fourteen --git-lfs --depth=1 
git clone https://github.com/username/local_manifest --depth 1 -b branch .repo/local_manifests && 

# Sync the repositories
/opt/crave/resync.sh  && 

# Set up build environment
source build/envsetup.sh && 
 
# Build the ROM
lunch lineage_codename-ap1a-variant && make installclean && mka bacon"
```
2. Only do repo init ROMs you think are related to each other.
3. **Don't sync another Android version over the current one.**

**Getting build outputs:**

1. Build completed? Congratulations on your success! Now you want your ROM files. It's so simple.
 
```
crave pull out/target/product/codename/romname.zip
```

## I guess that's it. In case you think that this guide is missing some more things, feel free to pull request or you can report an issue.