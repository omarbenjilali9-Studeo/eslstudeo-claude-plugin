---
name: connect-eslstudeo
description: Connects Claude to ESLStudeo and explains what the connection may see and do. Use this skill when the ESLStudeo tools are missing, when an ESLStudeo call is refused for lack of permission or an expired connection, or when the person asks how to connect ESLStudeo, what its permissions mean, what ESLStudeo shares with Claude, why Claude cannot see their classes or learners, or how to end the connection, for example "connect my ESLStudeo account", "why can't you see my classes?", "what can you access in ESLStudeo?" or "disconnect ESLStudeo".
---

# Connecting to ESLStudeo

ESLStudeo (eslstudeo.com) is a platform where people build courses and teach classes, in any
subject. This plugin reaches it through one connector at `https://eslstudeo.com/mcp`. The connector
acts as the ESLStudeo account that approved it, and only within what that account may already do in
ESLStudeo.

## 1. Check the connection

1. Look for the ESLStudeo tools, for example `list_my_courses` and `list_classes`.
2. **No ESLStudeo tools at all.** The connector is not connected. Tell the person:
   1. In Claude, open **Customize → Connectors**, find **ESLStudeo**, and press **Connect**. If
      ESLStudeo is not listed, the plugin is switched off or not installed: see **Customize → Plugins**.
   2. An ESLStudeo page opens. Sign in with the ESLStudeo email or username and password. The
      password goes to ESLStudeo and never to Claude.
   3. Read the list of what is being asked for. To let Claude work with classes and learners as
      well as courses, switch on **Also let it into your classes**; it starts off. Then press
      **Allow**.
3. **Course tools present, class tools missing** (`list_my_courses` works; `list_classes` does not
   exist). The connection holds only the course permissions: either the switch **Also let it into
   your classes** was left off, or the connection was approved before ESLStudeo offered the class
   tools. If the person wants the class tools, tell them to disconnect ESLStudeo in
   **Customize → Connectors**, connect again, and switch it on before pressing **Allow**.
4. **A call answers "This connection may not use …".** Same cause as step 3.
5. **A call answers that the key has expired or was ended, or that the account is not active.**
   The connection was ended in ESLStudeo, or the account changed. Connect again. An account that is
   not active must be restored in ESLStudeo first; in an organization, the head of the organization
   does that.

## 2. The four permissions

The ESLStudeo approval page lists these in plain words. The two course permissions are granted when
the person presses **Allow**; the two class permissions only if they also switched on **Also let it
into your classes**. Each permission unlocks a fixed set of tools.

| Permission | What it allows | Tools |
|---|---|---|
| See courses (`courses:read`) | Read the courses the person may edit, and everything written in them | `what_can_this_builder_do`, `list_my_courses`, `read_course`, `read_unit`, `read_page`, `find_in_course`, `list_versions`, `check_course` |
| Change courses (`courses:write`) | Create courses; write sections, units, pages and exercises; upload pictures and documents | `create_course`, `update_course`, `set_course_settings`, `add_section`, `update_section`, `add_unit`, `update_unit`, `set_unit_delivery`, `add_page`, `update_page`, `set_exercises`, `set_marking_guidance`, `move_item`, `duplicate_item`, `delete_item`, `replace_text`, `restore_version`, `upload_image`, `upload_file` |
| See classes and learners (`students:read`) | Read the person's classes and learners: names, marks, what each learner has and has not done, and email addresses where they exist | `list_classes`, `class_roster`, `class_progress`, `find_students`, `discussion_status` |
| Act in classes (`students:write`) | Create classes, and send learners notices inside ESLStudeo | `create_class`, `send_notice` |

Limits that no permission lifts:
- Only courses the person may already edit. A co-author with "propose" access writes proposals that
  wait for the course owner; `list_my_courses` says which courses work that way. A course licensed
  to an organization can be taught but not edited.
- Only classes the person may see in ESLStudeo: a teacher sees their own classes; the heads of an
  organization see its classes.
- Every change is recorded in ESLStudeo as made through the connector, by that person.
- ESLStudeo never sends email on anyone's behalf. Notices appear inside ESLStudeo.
- A whole course cannot be deleted through the connector; that is done in ESLStudeo itself.

## 3. What leaves ESLStudeo

Whatever an ESLStudeo tool returns is sent to Anthropic and handled under Anthropic's terms, not
ESLStudeo's. With the class permissions, this includes learners' names, marks and email addresses.
State this plainly the first time the person asks for learner information, and respect their choice.

- To build courses without Claude seeing any learner information, the person leaves **Also let it
  into your classes** off on the ESLStudeo page. On a connection that already has the class
  permissions, they can instead set the seven class tools (`list_classes`, `class_roster`,
  `class_progress`, `find_students`, `discussion_status`, `create_class`, `send_notice`) to
  **Blocked** in **Customize → Connectors → ESLStudeo → Tool permissions**.
- ESLStudeo labels each tool as reading or changing, so Claude's **Tool permissions** page groups
  them. Each group, or each tool, can be set to **Always allow**, **Needs approval** or **Blocked**.
  A sensible setting is **Always allow** for the reading tools and **Needs approval** for the
  changing ones; at the least, suggest **Needs approval** for `delete_item`, `restore_version`,
  `replace_text` and `send_notice` if the person wants Claude to stop and ask before those run.

## 4. Ending the connection

Either side ends it at once:
- In ESLStudeo: **⚙ → Connected apps** lists every connection the person has allowed, and ends any
  of them.
- In Claude: **Customize → Connectors → ESLStudeo → Disconnect**.

Removing the plugin removes these instructions together with the connector.

## 5. Other assistants

ChatGPT and other assistants can use the same address, `https://eslstudeo.com/mcp`, as a connector.
The permissions and the ESLStudeo approval page are the same there; only these instructions are
specific to Claude.
